## How is Uber changing Taxi in New York City?

Uber is a new riding model which connects drivers and passengers and provides ride-sharing service with a fair rate. This visualization tool enable user to analyze and compare Uber and taxi traffic of neighbors in NYC. 

To use the tool, you can clone this repository onto your computer and use the NYC_Uber_Taxi.html page.


### Organization of the  project

The project has the following structure:

    DATA515-Project/
      |- data/
         |- Taxi_samples/
            |- dimensions.txt
            |- taxi_04_2014_sample.csv
            |- taxi_05_2014_sample.csv
            |- taxi_06_2014_sample.csv
         |- Uber_samples/
            |- uber_04_2014_sample.csv
            |- uber_05_2014_sample.csv
            |- uber_06_2014_sample.csv
     	   |- NYC_Shapes.json
     	   |- NYC_Shapes_Cleaned.json     	 
      |- doc/
         |- Design_Specification_and_Project_Plan.pdf
         |- Functional_Specification.pdf
         |- Presentation_How_is_Uber_Changing_Taxi_in_New_York_City.pdf
         |- Technical_Review
      |- examples/
         |- EXAMPLES.md
      |- uberTaxi/
         |- script/
            |- check_points.py
            |- find_neighborhood.py
            |- geo_convert.py
            |- main.py
            |- process_coordinates.py
            |- queries.py
            |- random_sample.py
            |- read_json.py
            |- split_data.py
         |- test/
            |- TestAllFunction.py
      |- LICENSE
      |- README.md
      |- setup.py
      |- NYC_Uber_Taxi.html
      

### Project Data

#### Uber pick-up data

Uber data contains over 18 million Uber pickups in New York City from April to September 2014 and from January to June 2015. FiveThirtyEight originally obtained the data from the NYC Taxi & Limousine Commission (TLC) by submitting a Freedom of Information Law. We downloaded the dataset from Kaggle.com. The uber dataset contain pickup date and time, detailed location information, uber base code. 

#### NYC yellow taxi data

The yellow taxi trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts. The dataset is publicly available on: http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml



### Use Case 

#### Uber driver

Uber driver wants to figure out where to find more customers at a specific time of the day. For example, Tom is part-time uber driver. He lives in Long Island and he wants to find what time during the day there are the most pickups in his neighborhood or at a specific time, where to find more business.

#### Passanger

Passenger wants to compare the availability of Uber and taxi, and make a decision. For example, David is a passenger. He plans to visit NYC next week. He enjoys night life and stay in the pub 3am. It is hard to request a ride at that time. He wants to use our application to decide whether Uber or taxi has more availability at that time.

#### Taxi company 

Taxi company studies their business strategies for the next year. For example, Happytaxi is taxi company based in NYC. They want to figure out how Uber affect taxi traffic. So that they can decide how many taxicab they should purchase next year.



### Design
#### Componets

Regional Heat Map

Regional heat map summarizes and aggregates data within pre-defined hundreds of neighborhoods in New York City. Initially, it displays community district boundaries and color of this neighborhood generates by corresponding number of pickups. Without making any selections, users can have a general overview of what kind of information they can have from heat map by simply hover over it. When a user hovers over a neighborhood, it displays a popup containing neighborhood name, number of pickups in this neighborhood and geographic coordinates of current point. 

Filter Options

The filter options allow users to select between Uber and taxi as well as a certain period they feel they are most interested in. Filters include a checkbox button group, a slider and two dropdown menus. Checkbox button group provides selections between Uber and taxi. The initial value is Uber data on April 1st at hour 0. Users can select either some of the filters or all of the filters. If only some of filters are selected, then the others will keep their initializing defaults.

#### Interaction
The complete interaction process of our tool is: 

User first select the month, date, hour, and uber/taxi indicator as inputs and system prepare the SQL statements. Then through pyodbc, the database will execute the query and return a demanded collection of records containing the aggregated pickup number. We transformed this collection into a matrix that can be loaded into the source of bokeh heatmap. By reading the NYC shape boundaries data and the matrix we just transformed, a bokeh heatmap will be generated in python and the color on the heatmap encodes the aggregated pickup number. Finally, four filters are appened to allow some interactions. The connection between heatmap and filters is achieved by Javascript Callbacks, which is an advanced topic that we spent a large of time to understand and implement it successfully.   
Basically, to summarize, the Bokeh heatmap provides the main interface of our visualization. Database provides what to display in the main interface, and fours filters connected to the heatmap control the display.


### Limitation and Future Work
* Connect to Uber API
* Use more recent data and data from more cities
* Enable narrow down to street level


