# Stock Analysis with VBA

## Project Overview
This project includes a set of Visual Basic Applications (VBA) code that was written to analyze a given group of stocks. The task at hand is to refactor the VBA code for more efficient execution.

### Purpose
The purpose of this project is to provide the client with a tool, a VBA script that will analyze a set of Wall Street stock and provide information regarding their performance, specifically the Total Daily Volume and the Return for the given years 2017 and 2018.

## Methods
An Excel spreadsheet was provided that contained the trading volume and closing value for a selection of 12 Wall Street stock symbols. The spreadsheet included data for the years 2017 and 2018. VBA code was written to summarize and extract the total volume and the loss/gain data for the selected stocks. Furthermore, a timer was implemented to compare the execution speeds of the two sets of code, Original and Refactored. The elapsed time will be displayed at the end of the analysis via a pop up window.

### Original Code
The original code set was set up as outlined below.
1. An input box was created to capture the desired analysis year.
2. The output headers were created and formatted to include a section header and a header row.
3. Initialized the stock symbols array and assigned each of the twelve symbols to an array element.
4. Prepared for the analysis by initializing the variables for the stock starting price, stock ending price, and the number of total rows in the data set.
5. Created a nested FOR loop to collect the Starting Price, Ending Price, and the Total Volume for each of the desired stocks.
6. The data was written to the output worksheet under the headings created in step 2.
7. Formatted the output data for better readability. 

### Refactored Code
The refactoring was done to the original code to produce a more efficient process for the analysis.  The steps are described in the list below. Steps 1 - 3 were preserved from the original code. Changes were implemented beginning from step 4 onwards.
4. A stock ticker index was created to track the Stock, Starting Price, Ending Price, and the Trading Volume.
5. Created a loop to initialize the total volume per each stock to the value of zero.
6. A second loop was created to loop over the data rows of the full data set of the desired year and collect the starting price, ending price, and the total volumes per each of the stock symbols.
7. Created a loop to output the stock symbol, stock volume, and return on stock under the output headers created under step 2.
8. Formatted the output data for better readability.

## Results

### Numerical Results
As expected, both the Original and Refactored code produced identical numerical results for the traded volumes and return on stocks.

For the year of 2017, the most traded stock within the twelve stocks analyzed was FSLR with a total volume of 684,181,400 which returned a gain of 101.3 percent. The stock with symbol DQ traded a total volume of 35,796,200 with a return of 199.4 percent. On the low end of the scale for return was the stock TERP with a total volume of 139,402,800 stocks traded with a negative return of 7.2 percent.

The 2018-year analysis showed two of the stock ENPH and RUN were the only stock that yielded a positive return. ENPH returned 81.9 percent with a traded volume of 607,473,500 and RUN returned 84.0 percent with a total volume of 502,757,100 in trade.

### Code Performance
When comparing the execution speeds of the Original and Refactored VBA code, it was visibly evident that the refactored code performs better by far. The execution times for the Original and Refactored code is presented below as evidence to the fact. The blocks of code below shows the changes that were made in improving the performance in the Refactored version.

Original version Nested Loop for the summary and calculations

For i = 0 To 11
        ticker = tickers(i)
        totalVolume = 0
        
        Worksheets(yearValue).Activate
        For j = 2 To RowCount
    
            If Cells(j, 1).Value = ticker Then
                totalVolume = totalVolume + Cells(j, 8).Value
            End If
    
            If Cells(j, 1).Value = ticker And Cells(j - 1, 1).Value <> ticker Then
                startingPrice = Cells(j, 6).Value
            End If
    
            If Cells(j, 1).Value = ticker And Cells(i + 1, 1).Value <> ticker Then
                endingPrice = Cells(j, 6).Value
            End If
        Next j
    
        Worksheets("All Stocks Analysis").Activate
        Cells(i + 4, 1).Value = ticker
        Cells(i + 4, 2).Value = totalVolume
        Cells(i + 4, 3).Value = endingPrice / startingPrice - 1
    Next i

Refactored version with separated functional loops

    tickerIndex = 0

    
    Dim tickerVolumes(11) As Long
    Dim tickerStartingPrice(11) As Single
    Dim tickerEndingPrice(11) As Single
    
    
    For i = 0 To 11
        tickerVolumes(i) = 0
    Next i

    For i = 2 To RowCount
    
        tickerVolumes(tickerIndex) = tickerVolumes(tickerIndex) + Cells(i, 8).Value
        
        If Cells(i, 1).Value = tickers(tickerIndex) And Cells(i - 1, 1) <> tickers(tickerIndex) Then
            tickerStartingPrice(tickerIndex) = Cells(i, 6).Value
        End If

        If Cells(i, 1).Value = tickers(tickerIndex) And Cells(i + 1, 1) <> tickers(tickerIndex) Then
            tickerEndingPrice(tickerIndex) = Cells(i, 6).Value
            
            tickerIndex = tickerIndex + 1
            
        End If
    
    Next i
    
    For i = 0 To 11
        
        Worksheets("All Stocks Analysis").Activate
        Cells(i + 4, 1).Value = tickers(i)
        Cells(i + 4, 2).Value = tickerVolumes(i)
        Cells(i + 4, 3).Value = tickerEndingPrice(i) / tickerStartingPrice(i) - 1
        
    Next i

#### Original
2017 Original Code Performance

![Year_2017_Original_Code_Performance](Resources/Original_2017.PNG)

2018 Original Code Performance

![Year_2018_Original_Code_Performance](Resources/Original_2018.PNG)

#### Refactored
2017 Refactored Code Performance

![Year_2017_Refactored_Code_Performance](Resources/VBA_Challenge_2017.png)

2018 Refactored Code Performance

![Year_2018_Refactored_Code_Performance](Resources/VBA_Challenge_2018.png)

## Summary
1.  What are the advantages or disadvantages of refactoring?
    - Advantage => The code performs more efficiently.
    - Advantage => The code is more reliable.
    - Advantage => The code structure is much cleaner and easier to read.
    - Advantage => Reduced complexity.
    - Advantage => Easier to maintain.
    - Disadvantage => Takes longer to write and implement.
2. How do these pros and cons aply to refactoring the original VBA script?
    - The above listed advantges allow us to submit to the client our best possible solution with improved execution that provides reliable data.
    - The disadvantage listed above may lead us to a situation where we are at risk of not knowing how best to proceed and what revision is the best posible outcome.

## Conclusions
The conclusions drawn for this project are...
- The variation in the stock markets is so much that care should be taken in investing in any stock.
- Professional advisors should be sought out before investing in the stock market.
- VBA code can be written in many ways to achieve a given result.
- We should strive to produce code that is effcient in performing the analysis and calculation to the best of our ability.