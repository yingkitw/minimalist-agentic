# minimal-agentic

would like to build an agentic generative AI from scratch.

will only use the basic watsonx.ai api.

## Pattern

target to implement 4 pattern

### 1) Reflection

it is about using review and revise to improve the generation outcome

Sample Input

> plan a trip to jakarta for 3 days

Naive output

```text
 Sure, here's a basic plan for your trip to Jakarta:

Day 1:
- Start your day with a visit to the National Monument (Monas), which is a significant landmark in Jakarta.
- Next, head to the Istiqlal Mosque, one of the largest mosques in Southeast Asia.
- In the afternoon, explore the Fatahillah Square, a historic area with colonial architecture and local markets.
- End your day with a visit to the Ancol Beach, where you can enjoy the sunset and local seafood.

Day 2:
- Begin your day at the Jakarta Old Town (Kota Tua), where you can see Dutch colonial architecture and visit the Museum of Fine Arts and Ceramics.
- After lunch, head to the Jakarta Cathedral and the nearby Chinatown for shopping and food.
- In the evening, enjoy a traditional Wayang Kulit puppet show.

Day 3:
- Spend your morning at the Jakarta Zoo or the Ragunan Zoo, depending on your preference.
- After lunch, visit the Taman Mini Indonesia Indah, a cultural park that showcases various regions of Indonesia.
- End your trip with a visit to the Thousand Islands (Kepulauan Seribu), a group of small islands known for their beautiful beaches and snorkeling spots.
```

Review output

```text
The draft provides a well-structured itinerary for a trip to Jakarta, covering historical sites, cultural experiences, and recreational activities. However, there are a few points that could be improved for clarity and logical flow:

1. Day 1: The order of visits could be adjusted for better flow. Consider starting with the Old Town (Kota Tua) to immerse yourself in the local culture and history before moving on to the more modern Monas.

2. Day 2: The Jakarta Animal Park and Ancol Dreamland theme park are quite far from each other. You might want to suggest a different activity or a more central location for the afternoon to avoid travel time.

3. Day 3: The Fatahillah Square and Jakarta Maritime Museum are both interesting places, but they might not provide a very relaxing stroll as suggested. Consider recommending a different activity or location for the end of the trip.

4. General suggestion: Include some information about local transportation options and safety tips for tourists. This will make the draft more comprehensive and helpful for readers.
```

Revised output

```text
Here's a revised plan for your trip to Jakarta:

Day 1:
- Kickstart your journey by exploring the Old Town (Kota Tua), where you can immerse yourself in the local culture and history. Enjoy a meal at one of the many warungs (small eateries) and try some traditional Indonesian dishes.
- After lunch, head to the National Monument (Monas), a significant landmark in Jakarta.
- In the evening, catch a traditional dance performance at the Jakarta Cathedral or the Istiqlal Mosque.

Day 2:
- Begin your day at the Jakarta Animal Park, where you can see a variety of Indonesian wildlife.
- For lunch, consider visiting the Glodok Chinatown area, known for its diverse food scene.
- After lunch, visit the Ancol Dreamland theme park for some fun and entertainment. Alternatively, you could explore the nearby Ancol Beach, which offers a more relaxed atmosphere.
- In the evening, explore the nightlife at the Thamrin City shopping mall or the SCBD business district.

Day 3:
- Spend your morning at the Fatahillah Square, a historic square that hosts various cultural events and markets.
- Next, visit the Jakarta Maritime Museum to learn about the city's maritime history.
- To wrap up your trip, consider taking a leisurely boat ride around the nearby Thousand Islands, which offer beautiful views and a chance to relax.

General suggestions:
- Jakarta has an extensive public transportation system, including buses, minibuses (angkot), taxis, and the commuter rail (KRL Commuter). Consider using these options to get around the city.
- Always be cautious when using public transportation and keep your belongings secure.
- It's also recommended to have some local currency (Indonesian Rupiah) on hand, as not all establishments accept credit cards.
- Lastly, respect local customs and traditions during your visit to ensure a pleasant and memorable experience.
```

### 2) Use Tool

it is about using tool to acquire external data and proceed operation to external system.

#### a few consider when use tool

1) trust on code and tool over the memory.
2) you can use the tool provided, likely be well tested and reliable. you can consolidate all output to the context for the model to do final touch as summarization. but to pass outcome from one tool to another is not trivial.
3) you can also ask the model to generate the code on the spot, but you need more turn to help debug and revise the code since it may not fully reliable.

test case - external data (wikipedia)

input

> how deep is Mariana Trench

naive output

> The Mariana Trench, located in the western Pacific Ocean, is approximately 36,070 feet (10,994 meters) deep at its deepest point, known as the Challenger Deep. This makes it the deepest part of the world's oceans.

use tool output

> calling query_wikipedia({'topic': 'Mariana Trench'})...
> The Mariana Trench, located in the western Pacific Ocean, is the deepest oceanic trench on Earth. Its maximum known depth is 10,984 ± 25 meters (36,037 ± 82 feet; 6,006 ± 14 fathoms; 6.825 ± 0.016 miles). This depth is more than 2 kilometers (1.2 miles) farther from sea level than the peak of Mount Everest. The pressure at the bottom of the trench is 1,086 bar (15,750 psi), and the temperature ranges from 1 to 4 degrees Celsius (34 to 39 degrees Fahrenheit). One-celled organisms called monothalamea have been found at a record depth of 10.6 kilometers (35,000 feet; 6.6 miles) below the sea surface.

test case - near time data source (stock data)

input

> analysis the latest stock price of IBM

naive output

> As of my last update, I don't have real-time data or the ability to browse the internet. However, I can guide you on how to find the latest stock price of IBM. You can check financial websites like Yahoo Finance, Google Finance, or Bloomberg for the most recent stock prices. Please ensure you're using a reliable source and that the information is up-to-date.

use tool output

> calling get_stock_data({'ticker': 'IBM'})...
> Based on the provided knowledge, the latest stock price of IBM as of November 18, 2024, was $208.089996. This is the closing price for that day. The volume of shares traded on that day was 2658508. There were no dividends or stock splits reported for this period.

test case - real time data (world time)

input

> when it is now in Sydney

naive output

> The current time in Sydney, Australia is [insert current time here]. Please note that Sydney observes Daylight Saving Time from early October to early April, during which the time zone is UTC+10:30. The rest of the year, it follows UTC+11:00.

use tool output

> calling get_current_time({'location': 'Australia/Sydney'})...
> The current time in Sydney is 13:47:09 on November 19, 2024.

### 3) Multi Agent

it is about to employ different personale on generation or understanding.

### 4) Planning

it is about breakdown the goal into smaller pieces of task, that help to approach a big goal.

## Test Cases

### 1) 9.11 bigger than 9.8

it show case LLM not good on math, so it is not a reliable approach on math question.

### 2) how many R in straberry.

it show case LLM not good on counting.

### 3) how many prime number within 10000.

you cant ride on LLM to do this kind of math works.

### 4) when is the time now.

it show case LLM not have the latest information of the world, so it need to employ other tools to get those information.

## Environments

the lab will base on the [IBM watsonx.ai](http://watsonx.ai) and [IBM Granite 3 Model](https://www.ibm.com/new/ibm-granite-3-0-open-state-of-the-art-enterprise-models)
