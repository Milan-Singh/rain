# Basement Flooding

Looking at data for 311 calls around basement flooding. Data is not immediately
available on the Open Data Portal, but WBEZ FOIAed records from 2009 to 2015 for
a story in their Heat of the Moment series: [The Gross Gatherings](http://www.heatofthemoment.org/features/flood/)

The Center for Neighborhood Technology report referenced in the article has
additional information about how basement flooding disproportionately affects Chatham,
along with other neighborhoods in Chicago: [CNT RainReady Chatham](http://www.cnt.org/sites/default/files/publications/CNT_RainReady%20Community%20-%20Chatham.pdf)

## Updates

* After confirming that we received data with the same distribution as WBEZ,
it looks like aggregating calls to zip code hides the huge concentration of calls
in the Austin community area ([see notebook](Flooding Call Distribution.ipynb)).
* The distribution of basement flooding calls by zip code matches up very well with
FEMA disaster relief claims ([see notebook](FEMA and 311 Calls by Zip.ipynb)). Because
of this, it seems reasonable that the calls are an accurate picture of the actual
distribution of basement flooding (if not the total incidence).
* However, street flooding calls seem to fluctuate more across areas, and don't
line up as well to other data sources ([see notebook](Basement vs Street Flooding.ipynb)).
* [One presentation given by MWRD](https://www.mwrd.org/pv_obj_cache/pv_obj_id_3E3A3EB610DB06410C2605D11714E583525A7000/filename/12-18-2015_Seminar_Presentation.pdf) shows the potential distribution of the flood risk
output of their computer sewer model. Still need to confirm with MWRD, but it looks
like Austin is identified as having high risk, but not the South Side.
* From looking at potential relationships with housing data ([from Institute for Housing Studies](https://www.housingstudies.org/)), the clearest correlation
seems to be between basement flooding and number of foreclosures (2005-2015) in a
community area ([see notebook](IHS Data and Basement Flooding.ipynb)).

## 311 Data

As the result of a FOIA to 311, we received all calls to 311 for water in basement
flooding and water in street flooding from 2000 through mid-September of 2016. An
example of the data format is below, and location information is provided on a block
level, (i.e. 1200 W Cuyler Ave).

The data aggregated by zip code, neighborhood, ward, and community area (defined by
the [community areas on the Chicago Data Portal](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6))  as well as the date is in the
[311_data/](311_data/) folder. Additionally, because the data is split between calls
for "Water in Basement" and "Water in Street", it is also split into these categories
and aggregated. Files beginning with `wib` are for basement flooding, and files
beginning with `wos` are for street flooding.

### Data Usage

Because of potential privacy issues of releasing the data on an individual level,
we are not making the full dataset public, but aggregations by date and neighborhood/ward
are in the [311_data/](311_data/) folder.

However, if you're interested in running analyses or seeing different patterns in
the data, feel free to suggest analyses or write scripts processing the data based off
of the metadata below. We can run them on the data and share any results in aggregate
here.

### 311 Call Example Data

| Service Request No | Block Address | Created Date | Created Time | Call Type         | Latitude | Longitude |
|--------------------|---------------|--------------|--------------|-------------------|----------|-----------|
| 00-00000000        | 1100 Fake St  | Jan 01, 2000 | 12:00:00 AM  | Water in Basement | 40.00    | -87.00    |

## FEMA Data

Data from FEMA about disaster incidents, housing assistance for owners and renters,
public assistance applications, and registration intake for individuals in the housing
program for Cook County, Illinois flood and severe storm events are in the `fema_data`
directory. Further information about the data can be found here [FEMA Data Feeds](https://www.fema.gov/data-feeds)

The data other than the Disaster Declarations doesn't initially come with the
`incidentType` field, but this was added for ease of use, and to remove snow, tornado,
and other types of events.

## Data Analysis Questions

* What are the common characteristics of areas with high 311 calls?
* Are most of the calls condensed into isolated events, or are they distributed more
evenly?
* Given that 311 calls aren't a perfect measure for when flood events occurred,
can we use the FEMA data to get a more balanced picture of which areas have the
most flooding?
* Is there a certain threshold of rain that leads to basement flooding, or is it
more related to structural or environmental factors?
* Many of the calls seem concentrated in lower-income, majority black areas. Can
the pattern of flood reports be linked back to historical practices of redlining
and housing discrimination?
