# Weather API Visuals
This repository includes two Jupyter notebooks in the directory WeatherPy. The first of these notebooks is WeatherPy.ipynb. The code in this notebook will generate a random set of 1,500 separate longitudes and latitudes. It then queries the citipy library to find the nearest city by name to these random longitudes and latitudes. It creates a list of the unique city values from the random locations. Since the citipy database is somewhat limited, approximately 600 unique cities will likely be generated. 

The notebook then iterates through the list of cities, calling the openweathermap.org API to collect current weather for the individual cities. This includes, lat/long data, high temp for the day, relative humidity, percent cloud cover, wind speed, country, and a time stamp. Results are stored in a dataframe. If the city name is not found in openweathermap, then the city is skipped. This is accomplished using "try" and "except" functionality. The dataframe is then saved as a CSV for use in the next Jupyter notebook.

The last sections of the WeatherPy notebook analyze various weather trends, checking high temperatures as you move away from the equator in each hemisphere, humidity levels as you move away from the equator, cloud cover, and wind speed. Correlations are determined based on R^2 values, and likely explanations for the trends are discussed. Scatter plots are used to help with visualizing the trends.

The second notebook in the WeatherPy directory is VacationPy.ipynb. This notebook uses the CSV generated above to determine attractive destination spots based upon current weather across the globe. First, all cities resulting from the previous notebook are scatter plotted against a world map with dot size used to indicate relative humidity. Next, the dataset is filtered to only include the following:
* Cities where the high temp was between 20C and 26C
* Cities where cloud cover was under 10%
* Cities where the wind speed was less than 7 m/s
This dramatically reduces the number of likely destination spots for a quick vacation. Note that current weather is not necessarily indicative of future weather, so it would be a good idea to check the forecast for any candidate destinations you are considering. Finally, an API call to geoapify.com is placed in order to collect hotel information for the destination cities. The first hotel found within 10km of the center of the destination city is identified. A new visualization is generated that adds hotel name and country abreviation to the "hover over" functionality in the map.

![Candidate Destinations](output_data/destination_map.png)

### API's Used ###
Note that there you will need two API keys in order to utilize these notebooks. The first is a weather_api_key from OpenWeather.  One can generate an API key by following the instructions at:

https://openweathermap.org/faq

The second api key is for Geoapify.  One can generate an API key for Geoapify by following the instructions at login/sign up link at:

https://www.geoapify.com/

The two keys should be stored in a file called api_keys.py located in the WeatherPy subdirectory of your local repository. The keys should be called weather_api_key and geoapify_key respectively.
