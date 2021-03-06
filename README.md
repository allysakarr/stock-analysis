# VBA-stock-analysis
# Overview of Project
  My example client, Steve, is helping his parents out with their newest investment venture in green energy. Steve's parents want to invest all of their funds in one company based on the company stock ticker being "DQ" as his parents met at a Dairy Queen (DQ). Steve expressed some concern about this, and wants to run some analyses on the stocks of other green energy companies as well as the one that his parents have invested in to figure out where his parents' funds would be best allocated. 
  ## Purpose 
  The purpose of this project is to not only run an analysis on the DQ stock to show the total amount of shares that are traded daily (daily volume) along with the return percentage value, but also to run analyses on all the stocks of different green energy companies to compare the daily volumes and returns to see the different company results. This way, Steve's parents will have some detailed analysis in front of them to make a more educated decision on where to invest their money.
# Results
## DQ Stock Analysis
First, an analysis on the stock of the company "DQ" needs to be run as that is the primary company Steve's parents want to allocate their funds to. To do this, I began by making a separate worksheet to input the results of the DQ data analysis. From there, I activated the "2018" Worksheet as I wanted to gather my data from there and found the number of rows in Column A to loop over. I looped over all the rows, and then made a series of conditionals. These conditionals are to check the row ticker identity through the current row, the previous row and the following row. I have an example of the code I used below to loop over all the rows:

    'loop over all the rows
    For i = 2 To RowCount

        If Cells(i, 1).Value = "DQ" Then
            'increase totalVolume by the value in current row
            totalVolume = totalVolume + Cells(i, 8).Value
        End If
        If Cells(i - 1, 1).Value <> "DQ" And Cells(i, 1).Value = "DQ" Then
            'set starting price
            startingPrice = Cells(i, 6).Value
        End If
        If Cells(i + 1, 1).Value <> "DQ" And Cells(i, 1).Value = "DQ" Then
            'set ending price
            endingPrice = Cells(i, 6).Value
        End If
    Next i

I then input this into the DQ Analysis worksheet and calculated a return of -.626% for DQ, which means the stock for DQ dropped by 63%. To see these results, please view the "DQ Analysis" worksheet in this file: ![VBA_Challenge](https://github.com/allysakarr/stock-analysis/blob/master/VBA_Challenge.xlsm?raw=true).
## Analysis on All Stocks
Second, I ran an analysis on all the other companies using a similar methodology as I did for the DQ Analysis Worksheet. I wanted to include both years of Data availble, from 2017 and 2018, and I offered this as an Input Box in Excel to make the macro user-friendly. To check how long the macro takes to run, I included a timer. From here, I initialized some ticker arrays and some variables for both starting and ending prices. I used the same methodology from the previous analysis to create conditionals to get the total volume (total shares traded daily) for the current ticker, the starting price for the current ticker, and the ending price for the current ticker. I then put all this data into the new worksheet "All Stocks Analysis" to display the ticker, total Volume and the return value as a percentage. I also formatted this data so it would display as bolded and with different number formatting for readability. I made the data in the return column display as green if the return was positive and red if the return to negative to give more meaning behind the values displayed. I then closed the timer in the code and then provided a message box to display the results of the macro. 

The results of this analysis showed that in 2017, all companies had a positive return with the exception of company with the ticker "TERP". When the macro ran for 2018, all of the companies had a negative return except for the companies with tickers "ENPH" and "RUN". DQ, specifically had a positive return of 199.4% in 2017, meaninig they had a great monetary return. However, DQ had a return of -62.6% the following year in 2018, showing the largest drop of all the companies. To see these results, please view the "All Stocks Analysis" worksheet in this file: ![VBA_Challenge](https://github.com/allysakarr/stock-analysis/blob/master/VBA_Challenge.xlsm?raw=true).

## Refactored Analysis on All Stocks
Lastly, this code used to analyzed all the stocks needed to be refactored in order to accomodate more data and execute the macro more efficiently and quickly. In order to do this, I used similar code but refined it. I created a tickerIndex to use throughout the arrays, which were for the tickerVolumes, tickerStartingPrices and tickerEndingPrices. As I began to run my loop through all the tickers, the tickerIndex would be used as a constant to access the correct index throughout all of my conditionals. I then used the same logic as the previous analysis to loop through all of the arrays and output the "Ticker", "Total Daily Volume", and "Return" back into the All Stocks Analysis worksheet. Here is an example of that code to loop through the arrays and create these outputs:

    '4) Loop through your arrays to output the Ticker, Total Daily Volume, and Return.
        For i = 0 To 11
        
            Worksheets("All Stocks Analysis").Activate
            Cells(4 + i, 1).Value = tickers(i)
            Cells(4 + i, 2).Value = tickerVolumes(i)
            Cells(4 + i, 3).Value = tickerEndingPrices(i) / tickerStartingPrices(i) - 1
        
        Next i
This edit ultimately produced the same values as the previous analysis, showing DQ analysis as having the highest return in 2017 and the biggest drop in 2018 and the companies generally having a largely positive return in 2017 and largely negative return in 2018. However, this refactoring process led to the VBA code running much faster and efficiently.

To show this, I included a run button for the first code analyzing all the stocks along with another run button for the refactored code analyzing all the stocks. To see view these run buttons, please view the "All Stocks Analysis" worksheet in this file: ![VBA_Challenge](https://github.com/allysakarr/stock-analysis/blob/master/VBA_Challenge.xlsm?raw=true). You can clearly see the efficiency and speed increase in the 2017 year. For an example, I tested the run buttons and ran the first code in 0.671875 seconds for 2017 and ran the refactored code in 0.1210938 seconds for 2017. The values are generally around ~.6 seconds for the first code vs ~.12-.14 seconds for the refactored code. I have the message box displayed below:

![VBA_Challenge_2017.png](https://github.com/allysakarr/stock-analysis/blob/master/Resources/VBA_Challenge_2017.png?raw=true).

You also can see a clearly see a time decrease in code running through the year 2018. As an example, I tested the run bottoms again for 2018, showing a time of 0.671875 seconds for running the first code for 2018 and a time of 0.1328125 seconds for running the refactored code for 2018. The first code usually produces amounts aroubnd ~.6 seconds whereas the refactored code produces values around ~.12-.16 seconds. The message box with this information is displayed below: 

![VBA_Challenge_2018.png](https://github.com/allysakarr/stock-analysis/blob/master/Resources/VBA_Challenge_2018.png?raw=true)


# Summary 
To conclude these results for Steve, DQ dropped a large amount in 2018. I would advise Steve to encourage his parents to allocate their funds to other companies to get the best return on their investment. Specifically, the companies "ENPH" and "RUN" contiually had positive returns, meaning that I would recommend investing more in these companies over investing soley in DQ. 

In regards to refactoring the code as I did for efficiency and time-saving purposes, I recognize there can be pros and cons to this method. 

The advantage obviously would be that the code can run more efficiently, as we showed in the results section by comparing the speeds of the first code vs the refactored code. Changing the code in this way allowed for the code to be applied for larger data sets in a faster and more effective way, leading to a decrease in things like code smells and increase in code refinement.

However, there are disadvantages to approaching code in this way. By refactoring the code, the code has the potential to be altered in a negative way, leading to a potential decrease in functionality. It can become less specific and more generalized, leading to potentially ineffective code. Refactoring can also take longer, so if someone is on a time constraint with a project, refactoring might not be the best method to take when the goal is to produce quickly.

With these pros and cons in mind, it is important to consider the long term effect wanted from the code. Specifically for this project, I wanted Steve to have a code that he could apply to more than a dozen stocks. This code would need to be able to run efficiently and well with larger sets of data. With the first code, it was already somewhat "slow" for just 12 tickers. As one of its advantages though, it did run smoothly and successfully. With the refactored code, it substantially sped up the processing speed for the code to analyze the data. However, it took a lot of extra time to perfect a code that was already working. 

Ultimately, I am glad the first code was refactored as it matches Steve's needs the best by enabling the code to work faster and more efficiently with larger sets of data. However, if someone is more concerned with using up extra time vs developing code that performs better, it might be better to use code that is not refactored in order to have effective code and move on. It depends on the needs of the project, but I would refactor code when given the chance as I am a fan of making things perform better and more efficiently.
