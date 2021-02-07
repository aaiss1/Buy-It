# Buy-It

## Inspiration
These days, we’re all stuck at home, you know, cuz of COVID-19 and everything. 
If you’re anything like me, the lockdown has changed my online shopping habits quite a bit, and I find myself shopping on websites like Amazon way more than I used to.

With this change to my lifestyle, I realized that e-commerce is weirdly inconvenient when you really want to get the best price. You have to go check each retailer’s website individually, and compare prices manually. I then thought to myself, “Hey, it would be really cool if I had a price comparison tool to search for the best price across a variety of online retailers”. Before I knew it, I came up with Buy It, an application that does just that.

## What it does
Given a product name to search, Buy It will return search results from different online retailers giving you all the information you need to save money, all in one place.

## How I built it
Buy It is a mobile app developed in Android Studio using Java and Kotlin. The pricing data presented in the app is actually collected via web scraping. To do that, I leveraged the ParseHub API after training their scraping bot to search e-commerce websites with whatever product the user is interested in. The main issue is, the API isn’t easily compatible with Java, so I thought to host an API endpoint with Flask in Python to then make data available for my Java app to request. But I had a better idea: using Solace’s PubSub+ Event Broker. This made a lot of sense, since Solace’s event driven programming solution allows for easy two-way communication between both the client and the publisher. 

That means my app can send the user’s product search to the Python script, Python runs the API on that search to initiate a web scraping action, then Python also sends back whatever data it collects. Meanwhile, the Java app was simply waiting for messages on the topic of the search product. After receiving a response, it can then process the pricing information and display it to the user.

Another cool thing about using Solace is that it’s an extremely scalable solution. I could make this app track prices real time from a large number of retailers at once, in other words, I’d be generating constant heavy network traffic, and the event broker would have no issue. By leveraging PubSub+, I was able to make a quick, easy, and powerful communication pathway for all the components of my hack to talk through, while also future-proofing my app for further development and updates.

## Challenges we ran into
Unfortunately, I was not quite able to get the finishing touches in for this hack. The app was even able to receive the pricing information, it was just a matter of parsing it and displaying it in a user-friendly manner. With my only team member not being available to work with me last minute, this ended up being a solo hack programmed in Java and Python, languages I’ve never used before. That being said, the majority of it is done, and I put an immense amount of effort into learning all this.

## Accomplishments that we're proud of
I'm super excited about how much I've learned. I used Solace which was very useful and educational. I've also never built a mobile app, never done web scraping, never coded in Python or Java/Kotlin, so lots of new stuff. I was also impressed with my progress as a solo hack.

## What we learned
As previously mentioned, I learned how to build a mobile app in Android Studio with Java/Kotlin. I learned more about programming in Python (particularly API endpoints and such), as well as web scraping. Last but not least, I learned about Solace event brokers and how they can replace REST API endpoints.

## What's next for Buy It!
I was thinking of creating a watchlist, where the user can save items, which will subscribe the app to a topic that receives real-time price changes for said items. That way, the user is notified if the item is being sold below a certain price threshold. Because Buy It is built off of such a strong foundation with Solace, there’s lots of room for new features and enhancements, so I really look forward to getting creative with Buy It!
