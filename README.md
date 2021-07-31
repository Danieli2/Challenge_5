***Challenge_5****


**Background**


I decided to start a fintech consulting firm that focuses on projects to benefit local communities. I  won my first contract with a large credit union. The project entails building a tool to help credit union members evaluate their financial health. Specifically, the credit union board wants the members to be able to do two things. First, they should be able to assess their monthly budgets. Second, they should be able to forecast a reasonably effective retirement plan based on their current holdings of cryptocurrencies, stocks, and bonds. The chief technology officer (CTO) of the credit union wants me to develop a prototype application to present at its next assembly.

**What You're Creating**


I will create two financial analysis tools by using a single Jupyter notebook:
1. A financial planner for emergencies. The members will be able to use this tool to visualize their current savings. The members can then determine if they have    enough reserves for an emergency fund.
2. A financial planner for retirement. This tool will forecast the performance of their retirement portfolio in 30 years. To do this, the tool will make an          Alpaca API call via the Alpaca SDK to get historical price data for use in Monte Carlo simulations.

I will use the information from the Monte Carlo simulation to answer questions about the portfolio in my Jupyter Lab.

**Instructions**


This Challenge breaks the instructions into two parts. In Part 1, I build the financial planner for emergencies. In Part 2, I will build the financial planner for retirement.

Part 1: Create a Financial Planner for Emergencies
In this section, I create a personal financial planner for emergencies. To develop the prototype, I  assume the following:
1. The average monthly household income for each credit union member is $12,000.
2. Each credit union member has a savings portfolio that consists of a cryptocurrency wallet, stocks, and bonds.

I evaluated the Cryptocurrency Wallet by Using the Requests Library
In this section, I determined the current value of a member’s cryptocurrency wallet. I also collect the current prices for the Bitcoin and Ethereum cryptocurrencies by using the Python Requests library. For the prototype, I assumed that the members hold the 1.2 Bitcoins (BTC) and 5.3 Ethereum coins (ETH). To do all this, I complete the following steps:

1. I created a variable named monthly_income, and set its value to 12000.

2. I used the Requests library to get the current price (in US dollars) of Bitcoin (BTC) and Ethereum (ETH) by using the API endpoints that the starter code supplied.

3. I navigated the JSON response object to access the current price of each coin, and store each in a variable.



**Evaluate the Stock and Bond Holdings by Using the Alpaca SDK**

In this section, I determined the current value of a member’s stock and bond holdings. I made an API call to Alpaca via the Alpaca SDK to get the current closing prices of the SPDR S&P 500 ETF Trust (ticker: SPY) and of the iShares Core US Aggregate Bond ETF (ticker: AGG). For the prototype, I assumed that the member holds 110 shares of SPY, which represents the stock portion of their portfolio, and 200 shares of AGG, which represents the bond portion. To do all this,  I completed the following steps:

1. In the Starter_Code folder, I created an environment file (.env) to store the values of your Alpaca API key and Alpaca secret key.

2. I set the variables for the Alpaca API and secret keys. Using the Alpaca SDK, I created the Alpaca tradeapi.REST object. In this object, I included the parameters for the Alpaca API key, the secret key, and the version number.

3. I Set the following parameters for the Alpaca API call:

tickers: Use the tickers for the member’s stock and bond holdings.

timeframe: Use a time frame of one day.

start_date and end_date: Use the same date for these parameters, and format them with the date of the previous weekday (or 2020-08-07). This is because I wanted the one closing price for the most-recent trading day.

I get the current closing prices for SPY and AGG by using the Alpaca get_barset function. I then format the responses as a Pandas DataFrame by including the df property at the end of the get_barset function.

I then navigate the Alpaca response DataFrame, select the SPY and AGG closing prices, and store them as variables.

Following which I calculate the values, in US dollars, of the current amount of shares in each of the stock and bond portions of the portfolio, and print the results.

**Evaluate the Emergency Fund**


In this section, I used the valuations for the cryptocurrency wallet and for the stock and bond portions of the portfolio to determine if the credit union member has enough savings to build an emergency fund into their financial plan. To do this,  I completed the following steps:

1. I created a Python list named savings_data that has two elements. The first element contains the total value of the cryptocurrency wallet. The second element contains the total value of the stock and bond portions of the portfolio.

2. I used the savings_data list to create a Pandas DataFrame named savings_df, and then display this DataFrame. The function to create the DataFrame should take the following three parameters:

savings_data: Used the list that I just created.

columns: Set this parameter equal to a Python list with a single value called amount.

index: Set this parameter equal to a Python list with the values of crypto and stock/bond.

I used the savings_df DataFrame to plot a pie chart that visualizes the composition of the member’s portfolio. The y-axis of the pie chart uses amount. 

Using Python, I determined if the current portfolio has enough to create an emergency fund as part of the member’s financial plan. Ideally, an emergency fund should equal to three times the member’s monthly income. To do this, I implemented the following steps:

I created a variable named emergency_fund_value, and set it equal to three times the value of the member’s monthly_income of $12000. 

I created a series of three if statements to determine if the member’s total portfolio is large enough to fund the emergency portfolio



**Part 2: Create a Financial Planner for Retirement**


In this section, I used the Alpaca API to get historical closing prices for a retirement portfolio. I then ran Monte Carlo simulation to forecast the portfolio performance 30 years from now. I used the simulated data to answer questions in my Jupyter lab about the portfolio.

I used the starter code in financial_planning_tools.ipynb to complete the steps in the following subsections.

**Create the Monte Carlo Simulation**

In this section, I used the MCForecastTools library to create a Monte Carlo simulation for the member’s savings portfolio. To do this, I complete the following steps:

1. I made an API call via the Alpaca SDK to get 3 years of historical closing prices for a traditional 60/40 portfolio split: 60% stocks (SPY) and 40% bonds (AGG).

2. I ran a Monte Carlo simulation of 500 samples and 30 years for the 60/40 portfolio, and then plot the results. The following image shows the overlay line plot resulting from a simulation with these characteristics. 


3. I ploted the probability distribution of the Monte Carlo simulation. The following image shows the histogram plot resulting from a simulation with these characteristics.


4. I generated the summary statistics for the Monte Carlo simulation.


**New Monte Carlo simulation**

I forecasted the cumulative returns for 10 years from now. Because of the shortened investment horizon (30 years to 10 years), the portfolio needs to invest more heavily in the riskier asset—that is, stock—to help accumulate wealth for retirement.

I Adjusted the weights of the retirement portfolio so that the composition for the Monte Carlo simulation consists of 20% bonds and 80% stocks.

I ran the simulation over 500 samples, and used the same data that the API call to Alpaca generated.

Based on the new Monte Carlo simulation, I answer the following questions in your Jupyter Lab:

Question 1: Using the current value of only the stock and bond portion of the member's portfolio and the summary statistics that you generated from the new Monte Carlo simulation, what are the lower and upper bounds for the expected value of the portfolio (with the new weights) with a 95% confidence interval?

Question 2: Will weighting the portfolio more heavily toward stocks allow the credit union members to retire after only 10 years?
