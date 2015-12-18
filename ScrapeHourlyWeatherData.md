
# Scrape Hourly Weather Data

First, we need to import the correct libraries. Urllib2 helps us read the information on a URL. Pandas lets us manipulate data. BeautifulSoup helps us scrape the data


```python
import urllib2
import pandas as pd
from bs4 import BeautifulSoup
```

For this project, I only need weather information from April through November in the years 2014 and 2015. You can change the range if you need to.

I also ensure that I am not scraping the same date more than once, and that I account for leap years (I set this up even though one didn't happen.')

Then, I'll pull in the URL I am scraping, and for my particular task, I need to scrape data from the table at the bottom of the page. Then I compile all the information and add the date.


```python


weather_data = []
date = []
for y in range(2014,2016):
    for m in range(4, 12):
        for d in range(1, 32):
            #check if a leap year
            if y%400 == 0:
                leap = True
            elif y%100 == 0:
                leap = False
            elif y%4 == 0:
                leap = True
            else:
                leap = False
                            
            #check to see if dates have already been scraped	
            
            if (m==2 and leap and d>29):
                continue
            elif (y==2013 and m==2 and d > 28):
                continue
            elif(m in [4, 6, 9, 11] and d > 30):
                continue

            timestamp = str(y) + str(m) + str(d)
            print 'Getting data for ' + timestamp

#pull URL
            url = 'http://www.wunderground.com/history/airport/KMIC/' + str(y) + '/' + str(m) + '/' + str(d) + '/DailyHistory.html?HideSpecis=1'
            page = urllib2.urlopen(url)
        
        #find the correct piece of data on the page
            soup = BeautifulSoup(page)
            
            

            for row in soup.select("table tr.no-metars"):
                date.append(str(y) + '/' + str(m) + '/' + str(d))
                cells = [cell.text.strip().encode('ascii', 'ignore').decode('ascii') for cell in row.find_all('td')]
                weather_data.append(cells)
            
                    
```

    Getting data for 201441
    Getting data for 201442
    Getting data for 201443
    Getting data for 201444
    Getting data for 201445
    Getting data for 201446
    Getting data for 201447
    Getting data for 201448
    Getting data for 201449
    Getting data for 2014410
    Getting data for 2014411
    Getting data for 2014412
    Getting data for 2014413
    Getting data for 2014414
    Getting data for 2014415
    Getting data for 2014416
    Getting data for 2014417
    Getting data for 2014418
    Getting data for 2014419
    Getting data for 2014420
    Getting data for 2014421
    Getting data for 2014422
    Getting data for 2014423
    Getting data for 2014424
    Getting data for 2014425
    Getting data for 2014426
    Getting data for 2014427
    Getting data for 2014428
    Getting data for 2014429
    Getting data for 2014430
    Getting data for 201451
    Getting data for 201452
    Getting data for 201453
    Getting data for 201454
    Getting data for 201455
    Getting data for 201456
    Getting data for 201457
    Getting data for 201458
    Getting data for 201459
    Getting data for 2014510
    Getting data for 2014511
    Getting data for 2014512
    Getting data for 2014513
    Getting data for 2014514
    Getting data for 2014515
    Getting data for 2014516
    Getting data for 2014517
    Getting data for 2014518
    Getting data for 2014519
    Getting data for 2014520
    Getting data for 2014521
    Getting data for 2014522
    Getting data for 2014523
    Getting data for 2014524
    Getting data for 2014525
    Getting data for 2014526
    Getting data for 2014527
    Getting data for 2014528
    Getting data for 2014529
    Getting data for 2014530
    Getting data for 2014531
    Getting data for 201461
    Getting data for 201462
    Getting data for 201463
    Getting data for 201464
    Getting data for 201465
    Getting data for 201466
    Getting data for 201467
    Getting data for 201468
    Getting data for 201469
    Getting data for 2014610
    Getting data for 2014611
    Getting data for 2014612
    Getting data for 2014613
    Getting data for 2014614
    Getting data for 2014615
    Getting data for 2014616
    Getting data for 2014617
    Getting data for 2014618
    Getting data for 2014619
    Getting data for 2014620
    Getting data for 2014621
    Getting data for 2014622
    Getting data for 2014623
    Getting data for 2014624
    Getting data for 2014625
    Getting data for 2014626
    Getting data for 2014627
    Getting data for 2014628
    Getting data for 2014629
    Getting data for 2014630
    Getting data for 201471
    Getting data for 201472
    Getting data for 201473
    Getting data for 201474
    Getting data for 201475
    Getting data for 201476
    Getting data for 201477
    Getting data for 201478
    Getting data for 201479
    Getting data for 2014710
    Getting data for 2014711
    Getting data for 2014712
    Getting data for 2014713
    Getting data for 2014714
    Getting data for 2014715
    Getting data for 2014716
    Getting data for 2014717
    Getting data for 2014718
    Getting data for 2014719
    Getting data for 2014720
    Getting data for 2014721
    Getting data for 2014722
    Getting data for 2014723
    Getting data for 2014724
    Getting data for 2014725
    Getting data for 2014726
    Getting data for 2014727
    Getting data for 2014728
    Getting data for 2014729
    Getting data for 2014730
    Getting data for 2014731
    Getting data for 201481
    Getting data for 201482
    Getting data for 201483
    Getting data for 201484
    Getting data for 201485
    Getting data for 201486
    Getting data for 201487
    Getting data for 201488
    Getting data for 201489
    Getting data for 2014810
    Getting data for 2014811
    Getting data for 2014812
    Getting data for 2014813
    Getting data for 2014814
    Getting data for 2014815
    Getting data for 2014816
    Getting data for 2014817
    Getting data for 2014818
    Getting data for 2014819
    Getting data for 2014820
    Getting data for 2014821
    Getting data for 2014822
    Getting data for 2014823
    Getting data for 2014824
    Getting data for 2014825
    Getting data for 2014826
    Getting data for 2014827
    Getting data for 2014828
    Getting data for 2014829
    Getting data for 2014830
    Getting data for 2014831
    Getting data for 201491
    Getting data for 201492
    Getting data for 201493
    Getting data for 201494
    Getting data for 201495
    Getting data for 201496
    Getting data for 201497
    Getting data for 201498
    Getting data for 201499
    Getting data for 2014910
    Getting data for 2014911
    Getting data for 2014912
    Getting data for 2014913
    Getting data for 2014914
    Getting data for 2014915
    Getting data for 2014916
    Getting data for 2014917
    Getting data for 2014918
    Getting data for 2014919
    Getting data for 2014920
    Getting data for 2014921
    Getting data for 2014922
    Getting data for 2014923
    Getting data for 2014924
    Getting data for 2014925
    Getting data for 2014926
    Getting data for 2014927
    Getting data for 2014928
    Getting data for 2014929
    Getting data for 2014930
    Getting data for 2014101
    Getting data for 2014102
    Getting data for 2014103
    Getting data for 2014104
    Getting data for 2014105
    Getting data for 2014106
    Getting data for 2014107
    Getting data for 2014108
    Getting data for 2014109
    Getting data for 20141010
    Getting data for 20141011
    Getting data for 20141012
    Getting data for 20141013
    Getting data for 20141014
    Getting data for 20141015
    Getting data for 20141016
    Getting data for 20141017
    Getting data for 20141018
    Getting data for 20141019
    Getting data for 20141020
    Getting data for 20141021
    Getting data for 20141022
    Getting data for 20141023
    Getting data for 20141024
    Getting data for 20141025
    Getting data for 20141026
    Getting data for 20141027
    Getting data for 20141028
    Getting data for 20141029
    Getting data for 20141030
    Getting data for 20141031
    Getting data for 2014111
    Getting data for 2014112
    Getting data for 2014113
    Getting data for 2014114
    Getting data for 2014115
    Getting data for 2014116
    Getting data for 2014117
    Getting data for 2014118
    Getting data for 2014119
    Getting data for 20141110
    Getting data for 20141111
    Getting data for 20141112
    Getting data for 20141113
    Getting data for 20141114
    Getting data for 20141115
    Getting data for 20141116
    Getting data for 20141117
    Getting data for 20141118
    Getting data for 20141119
    Getting data for 20141120
    Getting data for 20141121
    Getting data for 20141122
    Getting data for 20141123
    Getting data for 20141124
    Getting data for 20141125
    Getting data for 20141126
    Getting data for 20141127
    Getting data for 20141128
    Getting data for 20141129
    Getting data for 20141130
    Getting data for 201541
    Getting data for 201542
    Getting data for 201543
    Getting data for 201544
    Getting data for 201545
    Getting data for 201546
    Getting data for 201547
    Getting data for 201548
    Getting data for 201549
    Getting data for 2015410
    Getting data for 2015411
    Getting data for 2015412
    Getting data for 2015413
    Getting data for 2015414
    Getting data for 2015415
    Getting data for 2015416
    Getting data for 2015417
    Getting data for 2015418
    Getting data for 2015419
    Getting data for 2015420
    Getting data for 2015421
    Getting data for 2015422
    Getting data for 2015423
    Getting data for 2015424
    Getting data for 2015425
    Getting data for 2015426
    Getting data for 2015427
    Getting data for 2015428
    Getting data for 2015429
    Getting data for 2015430
    Getting data for 201551
    Getting data for 201552
    Getting data for 201553
    Getting data for 201554
    Getting data for 201555
    Getting data for 201556
    Getting data for 201557
    Getting data for 201558
    Getting data for 201559
    Getting data for 2015510
    Getting data for 2015511
    Getting data for 2015512
    Getting data for 2015513
    Getting data for 2015514
    Getting data for 2015515
    Getting data for 2015516
    Getting data for 2015517
    Getting data for 2015518
    Getting data for 2015519
    Getting data for 2015520
    Getting data for 2015521
    Getting data for 2015522
    Getting data for 2015523
    Getting data for 2015524
    Getting data for 2015525
    Getting data for 2015526
    Getting data for 2015527
    Getting data for 2015528
    Getting data for 2015529
    Getting data for 2015530
    Getting data for 2015531
    Getting data for 201561
    Getting data for 201562
    Getting data for 201563
    Getting data for 201564
    Getting data for 201565
    Getting data for 201566
    Getting data for 201567
    Getting data for 201568
    Getting data for 201569
    Getting data for 2015610
    Getting data for 2015611
    Getting data for 2015612
    Getting data for 2015613
    Getting data for 2015614
    Getting data for 2015615
    Getting data for 2015616
    Getting data for 2015617
    Getting data for 2015618
    Getting data for 2015619
    Getting data for 2015620
    Getting data for 2015621
    Getting data for 2015622
    Getting data for 2015623
    Getting data for 2015624
    Getting data for 2015625
    Getting data for 2015626
    Getting data for 2015627
    Getting data for 2015628
    Getting data for 2015629
    Getting data for 2015630
    Getting data for 201571
    Getting data for 201572
    Getting data for 201573
    Getting data for 201574
    Getting data for 201575
    Getting data for 201576
    Getting data for 201577
    Getting data for 201578
    Getting data for 201579
    Getting data for 2015710
    Getting data for 2015711
    Getting data for 2015712
    Getting data for 2015713
    Getting data for 2015714
    Getting data for 2015715
    Getting data for 2015716
    Getting data for 2015717
    Getting data for 2015718
    Getting data for 2015719
    Getting data for 2015720
    Getting data for 2015721
    Getting data for 2015722
    Getting data for 2015723
    Getting data for 2015724
    Getting data for 2015725
    Getting data for 2015726
    Getting data for 2015727
    Getting data for 2015728
    Getting data for 2015729
    Getting data for 2015730
    Getting data for 2015731
    Getting data for 201581
    Getting data for 201582
    Getting data for 201583
    Getting data for 201584
    Getting data for 201585
    Getting data for 201586
    Getting data for 201587
    Getting data for 201588
    Getting data for 201589
    Getting data for 2015810
    Getting data for 2015811
    Getting data for 2015812
    Getting data for 2015813
    Getting data for 2015814
    Getting data for 2015815
    Getting data for 2015816
    Getting data for 2015817
    Getting data for 2015818
    Getting data for 2015819
    Getting data for 2015820
    Getting data for 2015821
    Getting data for 2015822
    Getting data for 2015823
    Getting data for 2015824
    Getting data for 2015825
    Getting data for 2015826
    Getting data for 2015827
    Getting data for 2015828
    Getting data for 2015829
    Getting data for 2015830
    Getting data for 2015831
    Getting data for 201591
    Getting data for 201592
    Getting data for 201593
    Getting data for 201594
    Getting data for 201595
    Getting data for 201596
    Getting data for 201597
    Getting data for 201598
    Getting data for 201599
    Getting data for 2015910
    Getting data for 2015911
    Getting data for 2015912
    Getting data for 2015913
    Getting data for 2015914
    Getting data for 2015915
    Getting data for 2015916
    Getting data for 2015917
    Getting data for 2015918
    Getting data for 2015919
    Getting data for 2015920
    Getting data for 2015921
    Getting data for 2015922
    Getting data for 2015923
    Getting data for 2015924
    Getting data for 2015925
    Getting data for 2015926
    Getting data for 2015927
    Getting data for 2015928
    Getting data for 2015929
    Getting data for 2015930
    Getting data for 2015101
    Getting data for 2015102
    Getting data for 2015103
    Getting data for 2015104
    Getting data for 2015105
    Getting data for 2015106
    Getting data for 2015107
    Getting data for 2015108
    Getting data for 2015109
    Getting data for 20151010
    Getting data for 20151011
    Getting data for 20151012
    Getting data for 20151013
    Getting data for 20151014
    Getting data for 20151015
    Getting data for 20151016
    Getting data for 20151017
    Getting data for 20151018
    Getting data for 20151019
    Getting data for 20151020
    Getting data for 20151021
    Getting data for 20151022
    Getting data for 20151023
    Getting data for 20151024
    Getting data for 20151025
    Getting data for 20151026
    Getting data for 20151027
    Getting data for 20151028
    Getting data for 20151029
    Getting data for 20151030
    Getting data for 20151031
    Getting data for 2015111
    Getting data for 2015112
    Getting data for 2015113
    Getting data for 2015114
    Getting data for 2015115
    Getting data for 2015116
    Getting data for 2015117
    Getting data for 2015118
    Getting data for 2015119
    Getting data for 20151110
    Getting data for 20151111
    Getting data for 20151112
    Getting data for 20151113
    Getting data for 20151114
    Getting data for 20151115
    Getting data for 20151116
    Getting data for 20151117
    Getting data for 20151118
    Getting data for 20151119
    Getting data for 20151120
    Getting data for 20151121
    Getting data for 20151122
    Getting data for 20151123
    Getting data for 20151124
    Getting data for 20151125
    Getting data for 20151126
    Getting data for 20151127
    Getting data for 20151128
    Getting data for 20151129
    Getting data for 20151130


Put associated data into a data frame using pandas


```python
weather_datadf = pd.DataFrame(weather_data)
datedf = pd.DataFrame(date)
```


```python
result = pd.concat([datedf, weather_datadf], axis=1)
result
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014/4/1</td>
      <td>12:53 AM</td>
      <td>32.0F</td>
      <td>24.2F</td>
      <td>28.9F</td>
      <td>88%</td>
      <td>29.43in</td>
      <td>2.5mi</td>
      <td>South</td>
      <td>9.2mph</td>
      <td>-</td>
      <td>0.00in</td>
      <td>Rain</td>
      <td>Light Freezing Rain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014/4/1</td>
      <td>1:53 AM</td>
      <td>30.0F</td>
      <td>23.2F</td>
      <td>28.0F</td>
      <td>92%</td>
      <td>29.44in</td>
      <td>4.0mi</td>
      <td>South</td>
      <td>6.9mph</td>
      <td>-</td>
      <td>0.00in</td>
      <td></td>
      <td>Overcast</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014/4/1</td>
      <td>2:53 AM</td>
      <td>30.9F</td>
      <td>25.2F</td>
      <td>28.0F</td>
      <td>89%</td>
      <td>29.47in</td>
      <td>3.0mi</td>
      <td>SW</td>
      <td>5.8mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014/4/1</td>
      <td>3:53 AM</td>
      <td>26.1F</td>
      <td>11.0F</td>
      <td>21.9F</td>
      <td>84%</td>
      <td>29.52in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>24.2mph</td>
      <td>32.2mph</td>
      <td>0.00in</td>
      <td></td>
      <td>Overcast</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014/4/1</td>
      <td>4:53 AM</td>
      <td>24.1F</td>
      <td>8.7F</td>
      <td>18.0F</td>
      <td>77%</td>
      <td>29.59in</td>
      <td>10.0mi</td>
      <td>NW</td>
      <td>23.0mph</td>
      <td>29.9mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2014/4/1</td>
      <td>5:53 AM</td>
      <td>23.0F</td>
      <td>8.0F</td>
      <td>16.0F</td>
      <td>74%</td>
      <td>29.65in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>20.7mph</td>
      <td>33.4mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2014/4/1</td>
      <td>6:53 AM</td>
      <td>21.0F</td>
      <td>4.6F</td>
      <td>14.0F</td>
      <td>74%</td>
      <td>29.72in</td>
      <td>9.0mi</td>
      <td>WNW</td>
      <td>23.0mph</td>
      <td>29.9mph</td>
      <td>0.00in</td>
      <td>Snow</td>
      <td>Light Snow</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2014/4/1</td>
      <td>7:53 AM</td>
      <td>19.9F</td>
      <td>4.3F</td>
      <td>12.9F</td>
      <td>74%</td>
      <td>29.78in</td>
      <td>4.0mi</td>
      <td>WNW</td>
      <td>19.6mph</td>
      <td>31.1mph</td>
      <td>0.00in</td>
      <td>Snow</td>
      <td>Light Snow</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2014/4/1</td>
      <td>8:53 AM</td>
      <td>19.9F</td>
      <td>3.5F</td>
      <td>15.1F</td>
      <td>81%</td>
      <td>29.81in</td>
      <td>0.8mi</td>
      <td>NW</td>
      <td>21.9mph</td>
      <td>27.6mph</td>
      <td>0.00in</td>
      <td>Snow</td>
      <td>Light Snow</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2014/4/1</td>
      <td>9:53 AM</td>
      <td>21.0F</td>
      <td>5.0F</td>
      <td>14.0F</td>
      <td>74%</td>
      <td>29.86in</td>
      <td>1.8mi</td>
      <td>NW</td>
      <td>21.9mph</td>
      <td>26.5mph</td>
      <td>0.00in</td>
      <td>Snow</td>
      <td>Light Snow</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2014/4/1</td>
      <td>10:53 AM</td>
      <td>24.1F</td>
      <td>9.0F</td>
      <td>15.1F</td>
      <td>69%</td>
      <td>29.89in</td>
      <td>3.0mi</td>
      <td>WNW</td>
      <td>21.9mph</td>
      <td>29.9mph</td>
      <td>0.00in</td>
      <td></td>
      <td>Haze</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2014/4/1</td>
      <td>11:53 AM</td>
      <td>27.0F</td>
      <td>14.7F</td>
      <td>16.0F</td>
      <td>63%</td>
      <td>29.94in</td>
      <td>10.0mi</td>
      <td>NW</td>
      <td>16.1mph</td>
      <td>26.5mph</td>
      <td>N/A</td>
      <td></td>
      <td>Scattered Clouds</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2014/4/1</td>
      <td>12:53 PM</td>
      <td>30.0F</td>
      <td>18.7F</td>
      <td>17.1F</td>
      <td>59%</td>
      <td>29.95in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>16.1mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Mostly Cloudy</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2014/4/1</td>
      <td>1:53 PM</td>
      <td>32.0F</td>
      <td>21.6F</td>
      <td>18.0F</td>
      <td>56%</td>
      <td>29.96in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>15.0mph</td>
      <td>21.9mph</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2014/4/1</td>
      <td>2:53 PM</td>
      <td>34.0F</td>
      <td>23.4F</td>
      <td>19.9F</td>
      <td>56%</td>
      <td>29.96in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>17.3mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Partly Cloudy</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2014/4/1</td>
      <td>3:53 PM</td>
      <td>37.0F</td>
      <td>28.5F</td>
      <td>23.0F</td>
      <td>57%</td>
      <td>29.98in</td>
      <td>10.0mi</td>
      <td>West</td>
      <td>13.8mph</td>
      <td>21.9mph</td>
      <td>N/A</td>
      <td></td>
      <td>Partly Cloudy</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2014/4/1</td>
      <td>4:53 PM</td>
      <td>35.1F</td>
      <td>24.5F</td>
      <td>21.9F</td>
      <td>59%</td>
      <td>29.99in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>18.4mph</td>
      <td>21.9mph</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2014/4/1</td>
      <td>5:53 PM</td>
      <td>36.0F</td>
      <td>28.0F</td>
      <td>23.0F</td>
      <td>59%</td>
      <td>30.01in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>11.5mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2014/4/1</td>
      <td>6:53 PM</td>
      <td>34.0F</td>
      <td>25.0F</td>
      <td>23.0F</td>
      <td>64%</td>
      <td>30.05in</td>
      <td>10.0mi</td>
      <td>West</td>
      <td>12.7mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2014/4/1</td>
      <td>7:53 PM</td>
      <td>32.0F</td>
      <td>26.4F</td>
      <td>21.9F</td>
      <td>66%</td>
      <td>30.08in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>5.8mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2014/4/1</td>
      <td>8:53 PM</td>
      <td>30.9F</td>
      <td>22.8F</td>
      <td>21.9F</td>
      <td>69%</td>
      <td>30.10in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>9.2mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2014/4/1</td>
      <td>9:53 PM</td>
      <td>28.9F</td>
      <td>21.1F</td>
      <td>21.0F</td>
      <td>72%</td>
      <td>30.12in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>8.1mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2014/4/1</td>
      <td>10:53 PM</td>
      <td>28.0F</td>
      <td>21.7F</td>
      <td>21.0F</td>
      <td>75%</td>
      <td>30.13in</td>
      <td>10.0mi</td>
      <td>WNW</td>
      <td>5.8mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2014/4/1</td>
      <td>11:53 PM</td>
      <td>27.0F</td>
      <td>19.5F</td>
      <td>19.9F</td>
      <td>75%</td>
      <td>30.14in</td>
      <td>10.0mi</td>
      <td>NW</td>
      <td>6.9mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2014/4/2</td>
      <td>12:53 AM</td>
      <td>27.0F</td>
      <td>18.7F</td>
      <td>17.1F</td>
      <td>66%</td>
      <td>30.16in</td>
      <td>10.0mi</td>
      <td>NNW</td>
      <td>8.1mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2014/4/2</td>
      <td>1:53 AM</td>
      <td>25.0F</td>
      <td>16.3F</td>
      <td>16.0F</td>
      <td>69%</td>
      <td>30.17in</td>
      <td>10.0mi</td>
      <td>NNW</td>
      <td>8.1mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2014/4/2</td>
      <td>2:53 AM</td>
      <td>23.0F</td>
      <td>15.8F</td>
      <td>15.1F</td>
      <td>72%</td>
      <td>30.17in</td>
      <td>10.0mi</td>
      <td>NNW</td>
      <td>5.8mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2014/4/2</td>
      <td>3:53 AM</td>
      <td>21.9F</td>
      <td>15.7F</td>
      <td>15.1F</td>
      <td>75%</td>
      <td>30.18in</td>
      <td>10.0mi</td>
      <td>NNW</td>
      <td>4.6mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2014/4/2</td>
      <td>4:53 AM</td>
      <td>21.0F</td>
      <td>16.2F</td>
      <td>14.0F</td>
      <td>74%</td>
      <td>30.19in</td>
      <td>10.0mi</td>
      <td>NW</td>
      <td>3.5mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2014/4/2</td>
      <td>5:53 AM</td>
      <td>19.0F</td>
      <td>12.3F</td>
      <td>14.0F</td>
      <td>81%</td>
      <td>30.19in</td>
      <td>10.0mi</td>
      <td>North</td>
      <td>4.6mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Clear</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11089</th>
      <td>2015/11/16</td>
      <td>4:53 AM</td>
      <td>54.0F</td>
      <td>46.0F</td>
      <td>75%</td>
      <td>29.86in</td>
      <td>10.0mi</td>
      <td>SSE</td>
      <td>16.1mph</td>
      <td>23.0mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11090</th>
      <td>2015/11/16</td>
      <td>5:53 AM</td>
      <td>53.1F</td>
      <td>46.0F</td>
      <td>77%</td>
      <td>29.85in</td>
      <td>10.0mi</td>
      <td>SE</td>
      <td>13.8mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11091</th>
      <td>2015/11/16</td>
      <td>6:53 AM</td>
      <td>52.0F</td>
      <td>46.0F</td>
      <td>80%</td>
      <td>29.85in</td>
      <td>8.0mi</td>
      <td>SSE</td>
      <td>10.4mph</td>
      <td>19.6mph</td>
      <td>0.00in</td>
      <td>Rain\n\t,\nThunderstorm</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11092</th>
      <td>2015/11/16</td>
      <td>7:53 AM</td>
      <td>52.0F</td>
      <td>45.0F</td>
      <td>77%</td>
      <td>29.85in</td>
      <td>10.0mi</td>
      <td>SSE</td>
      <td>11.5mph</td>
      <td>-</td>
      <td>0.03in</td>
      <td>Rain</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11093</th>
      <td>2015/11/16</td>
      <td>8:53 AM</td>
      <td>51.1F</td>
      <td>46.0F</td>
      <td>83%</td>
      <td>29.86in</td>
      <td>6.0mi</td>
      <td>SSE</td>
      <td>8.1mph</td>
      <td>-</td>
      <td>0.07in</td>
      <td>Rain</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11094</th>
      <td>2015/11/16</td>
      <td>9:53 AM</td>
      <td>51.1F</td>
      <td>45.0F</td>
      <td>80%</td>
      <td>29.84in</td>
      <td>10.0mi</td>
      <td>SE</td>
      <td>12.7mph</td>
      <td>18.4mph</td>
      <td>0.01in</td>
      <td>Rain</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11095</th>
      <td>2015/11/16</td>
      <td>10:53 AM</td>
      <td>48.9F</td>
      <td>45.0F</td>
      <td>86%</td>
      <td>29.83in</td>
      <td>2.5mi</td>
      <td>SE</td>
      <td>13.8mph</td>
      <td>-</td>
      <td>0.06in</td>
      <td>Rain</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11096</th>
      <td>2015/11/16</td>
      <td>11:53 AM</td>
      <td>48.9F</td>
      <td>45.0F</td>
      <td>86%</td>
      <td>29.80in</td>
      <td>5.0mi</td>
      <td>SSE</td>
      <td>12.7mph</td>
      <td>23.0mph</td>
      <td>0.07in</td>
      <td>Rain</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11097</th>
      <td>2015/11/16</td>
      <td>12:53 PM</td>
      <td>48.9F</td>
      <td>45.0F</td>
      <td>86%</td>
      <td>29.78in</td>
      <td>8.0mi</td>
      <td>SSE</td>
      <td>13.8mph</td>
      <td>-</td>
      <td>0.01in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11098</th>
      <td>2015/11/16</td>
      <td>1:53 PM</td>
      <td>48.9F</td>
      <td>46.0F</td>
      <td>90%</td>
      <td>29.77in</td>
      <td>1.2mi</td>
      <td>SE</td>
      <td>10.4mph</td>
      <td>19.6mph</td>
      <td>0.01in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11099</th>
      <td>2015/11/16</td>
      <td>2:53 PM</td>
      <td>48.9F</td>
      <td>46.0F</td>
      <td>90%</td>
      <td>29.78in</td>
      <td>1.2mi</td>
      <td>SE</td>
      <td>9.2mph</td>
      <td>-</td>
      <td>0.01in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11100</th>
      <td>2015/11/16</td>
      <td>3:53 PM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.78in</td>
      <td>1.8mi</td>
      <td>SE</td>
      <td>15.0mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11101</th>
      <td>2015/11/16</td>
      <td>4:53 PM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.78in</td>
      <td>9.0mi</td>
      <td>SSE</td>
      <td>15.0mph</td>
      <td>23.0mph</td>
      <td>0.00in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11102</th>
      <td>2015/11/16</td>
      <td>5:53 PM</td>
      <td>51.1F</td>
      <td>46.9F</td>
      <td>86%</td>
      <td>29.79in</td>
      <td>10.0mi</td>
      <td>SE</td>
      <td>16.1mph</td>
      <td>24.2mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11103</th>
      <td>2015/11/16</td>
      <td>6:53 PM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.81in</td>
      <td>10.0mi</td>
      <td>SSE</td>
      <td>13.8mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11104</th>
      <td>2015/11/16</td>
      <td>7:53 PM</td>
      <td>51.1F</td>
      <td>46.9F</td>
      <td>86%</td>
      <td>29.79in</td>
      <td>10.0mi</td>
      <td>SE</td>
      <td>15.0mph</td>
      <td>24.2mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11105</th>
      <td>2015/11/16</td>
      <td>8:53 PM</td>
      <td>51.1F</td>
      <td>46.9F</td>
      <td>86%</td>
      <td>29.80in</td>
      <td>10.0mi</td>
      <td>SSE</td>
      <td>15.0mph</td>
      <td>21.9mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11106</th>
      <td>2015/11/16</td>
      <td>9:53 PM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.79in</td>
      <td>10.0mi</td>
      <td>SSE</td>
      <td>13.8mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11107</th>
      <td>2015/11/16</td>
      <td>10:53 PM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.79in</td>
      <td>6.0mi</td>
      <td>SSE</td>
      <td>9.2mph</td>
      <td>21.9mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11108</th>
      <td>2015/11/16</td>
      <td>11:53 PM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.79in</td>
      <td>3.0mi</td>
      <td>SSE</td>
      <td>13.8mph</td>
      <td>-</td>
      <td>0.00in</td>
      <td>Rain</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11109</th>
      <td>2015/11/17</td>
      <td>12:53 AM</td>
      <td>50.0F</td>
      <td>48.0F</td>
      <td>93%</td>
      <td>29.78in</td>
      <td>5.0mi</td>
      <td>SE</td>
      <td>13.8mph</td>
      <td>18.4mph</td>
      <td>0.00in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11110</th>
      <td>2015/11/17</td>
      <td>1:53 AM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.75in</td>
      <td>8.0mi</td>
      <td>ESE</td>
      <td>9.2mph</td>
      <td>19.6mph</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11111</th>
      <td>2015/11/17</td>
      <td>2:53 AM</td>
      <td>50.0F</td>
      <td>46.9F</td>
      <td>89%</td>
      <td>29.74in</td>
      <td>7.0mi</td>
      <td>SE</td>
      <td>13.8mph</td>
      <td>20.7mph</td>
      <td>0.00in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11112</th>
      <td>2015/11/17</td>
      <td>3:53 AM</td>
      <td>51.1F</td>
      <td>48.0F</td>
      <td>89%</td>
      <td>29.75in</td>
      <td>6.0mi</td>
      <td>SE</td>
      <td>10.4mph</td>
      <td>-</td>
      <td>N/A</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11113</th>
      <td>2015/11/17</td>
      <td>4:53 AM</td>
      <td>51.1F</td>
      <td>48.0F</td>
      <td>89%</td>
      <td>29.69in</td>
      <td>6.0mi</td>
      <td>East</td>
      <td>13.8mph</td>
      <td>20.7mph</td>
      <td>0.12in</td>
      <td>Rain</td>
      <td>Light Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11114</th>
      <td>2015/11/17</td>
      <td>5:53 AM</td>
      <td>51.1F</td>
      <td>48.0F</td>
      <td>89%</td>
      <td>29.69in</td>
      <td>4.0mi</td>
      <td>ESE</td>
      <td>11.5mph</td>
      <td>18.4mph</td>
      <td>0.12in</td>
      <td>Rain</td>
      <td>Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11115</th>
      <td>2015/11/17</td>
      <td>6:53 AM</td>
      <td>51.1F</td>
      <td>48.0F</td>
      <td>89%</td>
      <td>29.70in</td>
      <td>6.0mi</td>
      <td>SE</td>
      <td>11.5mph</td>
      <td>18.4mph</td>
      <td>0.11in</td>
      <td>Rain</td>
      <td>Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11116</th>
      <td>2015/11/17</td>
      <td>7:53 AM</td>
      <td>51.1F</td>
      <td>48.0F</td>
      <td>89%</td>
      <td>29.70in</td>
      <td>1.8mi</td>
      <td>SE</td>
      <td>9.2mph</td>
      <td>-</td>
      <td>0.20in</td>
      <td>Rain</td>
      <td>Rain</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11117</th>
      <td>2015/11/17</td>
      <td>8:53 AM</td>
      <td>51.1F</td>
      <td>48.0F</td>
      <td>89%</td>
      <td>29.69in</td>
      <td>10.0mi</td>
      <td>SE</td>
      <td>12.7mph</td>
      <td>20.7mph</td>
      <td>0.07in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11118</th>
      <td>2015/11/17</td>
      <td>9:53 AM</td>
      <td>51.1F</td>
      <td>48.0F</td>
      <td>89%</td>
      <td>29.68in</td>
      <td>10.0mi</td>
      <td>SE</td>
      <td>10.4mph</td>
      <td>-</td>
      <td>0.02in</td>
      <td></td>
      <td>Overcast</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>11119 rows × 14 columns</p>
</div>



Write to a csv, and we're done!


```python
result.to_csv('weatherdata.csv')
```
