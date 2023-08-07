# tracing-llms
Tracing LLMs using LangSmith, Argilla, and other open-source tools

👉 LangSmith Walkthrough: https://python.langchain.com/docs/guides/langsmith/walkthrough  <br>
👉 Model Comparisons Walkthrough: https://python.langchain.com/docs/guides/model_laboratory


### To-do
- Google Palm LLM (from LangChain integration) is generating an itinerary by assigning 2hrs for each activity. This should be changed.
- Compare different LLMs' responses on itinerary generation using the default prompt templates. Prefer open-source LLMs.

### Prompts

User Prompt
```
query = f""" Plan a trip to {destination} from {arrival_date} to {departure_date} with ${budget}. 
        Start the itinerary from {start_time} to {end_time} for each day. 
        Keep in mind that {additional_info}.
        """

template = f"""{query}. Consider weather and budget, and include an estimated cost for each activity. The timings for each activity should be realistic.
        Display the ititenary in the following format: '\n\nTrip to <country/city/place>\n\nDay 1: <weather>\n<time-to-visit><things to do> or <places to visit> : \\<estimated cost>\n<time-to-visit><things to do> or <places           to visit> : \\<estimated cost>\n<time-to-visit><things to do> or <places to visit> : \\<estimated cost>\n<time-to-visit><things to do> or <places to visit> : <estimated cost>....\n\nDay N: <weather>\n<time-to-visit>          <things to do> or <places to visit> : <estimated cost>\n<time-to-visit><things to do> or <places to visit> : <estimated cost>\n<time-to-visit><things to do> or <places to visit> : <estimated cost>\n<time-to-visit>            <things to do> or <places to visit> : <estimated cost>\n\nTotal Estimated Cost: <total estimated cost>\n\nEnjoy your Trip!!!' 
        Don't include extra information.
        """
```

System Prompt
```
prompt = f" You are an expert at planning trips. \nGenerate a trip plan for this constraints: \n {user_query_template} \n The plan should contain day-to-day activities with timings. Be realistic, the places should exist and real. Include cost for each activity. \nThink about it step by step, use the tools to get weather data and generate an effective plan."
```


Tool Description:
```
description="use this tool for generating itinerary plan from the human input by considering weather"
```

