---
layout: default
title: OpenWeather
---

# OpenWeather Utility Bot Module

Certain dynamic information like the weather may be difficult or impossible to hard-code in AIML in advance. Enter bot modules, a handy solution for interfacing with third-party APIs, external knowledge or back-end databases, and more.

The OpenWeather Bot is a utility bot module that allows you to access [OpenWeatherMap.org](http://www.openweathermap.org/api) current weather information through their Weather API. *To request alpha access, email info at pandorabots dot com and include your [AIaaS](https://developer.pandorabots.com/) account name and application ID.*

Before getting started, familiarize yourself with the `<sraix>` [element](http://pandorabots.github.io/aiml/sraix/), and sign up for your own [free (or paid) plan](http://openweathermap.org/appid)  at OpenWeatherMap.org.

Note: when using utility bot modules to access third party APIs, in addition to needing an account with that service provider you should familiarize yourself with any rate or other limitations. Some third-party services may cause additional latency in bot responses.

### Initial Setup in your Bot Properties ###

We recommend creating bot properties to keep track of your specific values, such as

* Utility bot identifier - **utility/openweather**
* OpenWeather API Key - you must sign up for a weather API key at [OpenWeatherMap.org](http://openweathermap.org/appid)
* Units format - the OpenWeather utility bot supports units format: **imperial** (i.e. Fahrenheit, feet, etc), **metric** (Celsius, meters) or **kelvin**.
For example, try adding the following parameters to your bot properties file:

`["myweatherutilitybot","utility/openweather"],`
`["myweatherapikey","{appid}"],`
`["myunitsformat","imperial"],`

### Utility Bot Usage ###

CURRENT  *{query}* *{location}* OWMAPPID *{appid}* UNITSFORMAT *{metric, kelvin, or imperial}*

### Example Canonical Category ###

    <category>
      <pattern>XOPENWEATHER *</pattern>
      <template><sraix><bot><bot name="myweatherutilitybot"/></bot>CURRENT <star/> OWMAPPID <bot name="myweatherapikey" /> UNITSFORMAT <bot name="myunitsformat" /></sraix></template>
    </category>

### Queries ###

<table class="table table-striped table-bordered">
<tr><th>Query Description</th><th>Query Syntax</th></tr>
<tr><td>general weather condition (icon)</td><td>WEATHER <i>{location}</i></td></tr>
<tr><td>temperature (F, default or C, or Kelvin)</td><td>TEMP <i>{location}</i></td></tr>
<tr><td>cloudiness</td><td>CLOUDS <i>{location}</i></td></tr>
<tr><td>time of sunrise (UTC)</td><td>SUNRISE <i>{location}</i></td></tr>
<tr><td>time of sunset (UTC)</td><td>SUNSET <i>{location}</i></td></tr>
<tr><td>wind direction (cardinal)</td><td>WINDDIR <i>{location}</i></td></tr>
<tr><td>wind speed</td><td>WINDSPEED <i>{location}</i></td></tr>
<tr><td>atmospheric pressure (hPa)</td><td>PRESSURE <i>{location}</i></td></tr>
<tr><td>humidity (%)</td><td>HUMIDITY <i>{location}</i></td></tr>
<tr><td>visibility (feet, default or metric: meters)</td><td>VISIBILITY <i>{location}</i></td></tr>
<tr><td></td><td></td></tr>
</table>

#### Interaction Examples ####

**Input:** xopenweather weather mumbai  
**Output:** Sky is Clear  

**Input:** xopenweather temp beijing  
**Output:** 39.18    

**Input:** XOPENWEATHER WINDDIR DEATH VALLEY  
**Output:** SE  

**Input:** XOPENWEATHER Humidity Miami FL  
**Output:** 65  


### Guidelines ###

#### Alternate Responses: ####
Open Weather utility bot may respond in unexpected ways, such as:

* Invalid query: blank response
* Invalid units format: response returned in imperial format
* Ambiguous location: `Multiple Candidates. Please provide more information to narrow down`
For example, San Diego will return this response, so you would need to include more information, e.g. San Diego, TX or San Diego CA
* No information available for that query: `nil`

### Example Reductions: ###

You can reduce a natural language query to a open weather utility bot query. For example, using `<srai>` to your canonical category:

    <category>
      <pattern>WHAT IS THE CURRENT WEATHER IN *</pattern>
      <template><srai>XOPENWEATHER WEATHER <star /></srai></template>
    </category>

or if you want to return a different response:

    <category>
      <pattern>WHAT IS IT LIKE IN *</pattern>
      <template><srai>XOPENWEATHER CLOUDS <star/></srai></template>
    </category>

or if you want to make a change to units format for a single query:

    <category>
      <pattern>WHAT IS THE METRIC TEMP IN *</pattern>
      <template>
        <sraix><bot><bot name="myweatherutilitybot"/></bot>
			CURRENT TEMP <star/> OWMAPPID <bot name="myweatherapikey" /> UNITSFORMAT metric
		</sraix>
      </template>
    </category>

##### Interaction Examples: #####
*NOTE: these examples below assumes  you have standard normal.substitution file that processes contractions like "what's"*

**Input:** What's the current weather in Boston?  
**Output:** Multiple Candidates. Please provide more information to narrow down  

**Input:** What's the current weather in Boston, MA  
**Output:** scattered clouds  

**Input:** What's it like in Tokyo?  
**Output:** clear sky  

**Input:** What's the metric temp in Beijing?  
**Output:** 3.99  

*Last Updated: 3/16/2016*
