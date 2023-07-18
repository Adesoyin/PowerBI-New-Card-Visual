<img width="500" alt="image" src="https://github.com/Adesoyin/PowerBI-New-Card-Visual/assets/123065894/7868397f-b7d7-495a-8e8e-a090a21e26e2">

# PowerBI-New-Card-Visual

This gives an explanation of the new feature released by Power BI for the month of July 2023. 

**Overview**

This report was built to bring out the beautiful feature just added by Power BI for July 2023 update. You can interact with it using this link https://app.powerbi.com/view?r=eyJrIjoiOTIzOGRlN2QtZGU0OC00ZGUxLTk2ZGEtNTA1MjNkNGI3YzA1IiwidCI6IjM3ZDc1MjFhLTUwNzktNDhhZi05MTMxLTRhYzJjYjZmMWUzYSIsImMiOjF9 


**Tools and Properties used**
1. Power BI
2. Flaticon site to get all icons (https://www.flaticon.com)
3. Kerrykolosko site to get the sparklines measures (https://kerrykolosko.com/portfolio/sparklines/)
4. DAX measures
5. Slicers


**Get Data**

The data was gotten from the Power BI sample data which is financial data. It speaks to the units of product sold, the sales amount and the profit at the end of the day. The segment for the buyers and the country sold to. 

**Prepare the data**

Cleaning was not done as it came as cleaned data. However, the data types were changed to avoid errors in aggregating. 

![image](https://github.com/Adesoyin/PowerBI-New-Card-Visual/assets/123065894/823aca16-76fb-4fd0-9ed2-a27fd6616b93)

**Model the data**

The data loaded was previewed in the data view. A calender table was created using the function calenderauto(). The year, quarter and month were also created.
After which the month name (format(date[date],'mmm") was sorted out using the month number. 

![image](https://github.com/Adesoyin/PowerBI-New-Card-Visual/blob/main/Date%20Bata%20View.png)

And then, the Financial data was made related to the calendar table using the date field giving many to 1 relationship. 

![image](https://github.com/Adesoyin/PowerBI-New-Card-Visual/blob/main/Relationship.png)

**DAX Measures**

Different measures were created amongst which are Total Profit, Total Sales and Units Sold, all using sum aggregations. 

The Profit, unit sold and sales sparklines measures were computed as:

Profit Sparkline = 
            // Line and area colours - use %23 instead of # for Firefox compatibility (Measure Derived from Eldersveld Modified by Kolosko)

            // "Date" field used in this example along the X axis
            VAR XMinDate = MIN(financials[Date])
            VAR XMaxDate = MAX(financials[Date])
            
            // Obtain overall min and overall max measure values when evaluated for each date
            VAR YMinValue = MINX(Values(financials[Date]),CALCULATE([Profits]))
            VAR YMaxValue = MAXX(Values(financials[Date]),CALCULATE([Profits]))
            
            // Build table of X & Y coordinates and fit to 50 x 150 viewbox
            VAR SparklineTable = ADDCOLUMNS(
                SUMMARIZE('financials',financials[Date]),
                    "X",INT(150 * DIVIDE(financials[Date] - XMinDate, XMaxDate - XMinDate)),
                    "Y",INT(50 * DIVIDE([Profits] - YMinValue,YMaxValue - YMinValue)))
            
            // Concatenate X & Y coordinates to build the sparkline
            VAR Lines = CONCATENATEX(SparklineTable,[X] & "," & 50-[Y]," ", financials[Date])
            
            // Add to SVG, and verify Data Category is set to Image URL for this measure
            VAR SVGImageURL = 
                "data:image/svg+xml;utf8," & 
                "<svg xmlns='http://www.w3.org/2000/svg' x='0px' y='0px' viewBox='0 0 150 50'>" & 
                 "<polyline fill='white' fill-opacity='0.3' stroke='white' 
                  stroke-width='3' points=' 0 50 " & Lines & 
                  " 150 150 Z '/></svg>"
            RETURN SVGImageURL

These measures were saved as image url and selected under the image in the format feature of the visual, Placed below and size increased to 200 for proper alignment 

<img width="175" alt="image" src="https://github.com/Adesoyin/PowerBI-New-Card-Visual/assets/123065894/35ef1393-44f4-46a3-9ddf-225cdacf9411">

**Visualize the data**

In order to visualize the data, it is important to toggle on the "new card visual" in the preview feature of the Power BI settings. this can be found on the file tab- options & settings - preview feature. 

After this has been done, you can close the desktop and re-open it again to see the new feature

The card visual was selected and all measures calculated were placed and different icons were downloaded from the site and placed in each of the measures.

Likewise, the slicers' measures were also selected as images in the image format. Slicers were included to interact with the data. 

![image](https://github.com/Adesoyin/PowerBI-New-Card-Visual/blob/main/Report%20Page.png)

**In summary**

The new card is a great visual given by Microsoft to ease the stress of formatting and alignment. Likewise, a tool that gives access to the use of various formating such as the shape, color, image icon, image url, accent bar etc.


<img width="500" alt="image" src="https://github.com/Adesoyin/PowerBI-New-Card-Visual/assets/123065894/e81153b9-50e9-48a8-a062-9ea4549d14dc">



