# Kelly Yu's Midterm Project NYU DataBootcamp

**Intro:**

I designed this project to analyze stocks across different industries and their relationships with key macroeconomic factors. Ultimately, my guiding question was simple yet fundamental: How can I make more money when investing stocks? What’s the best investing strategy? Of course, the answer depends not on luck, but on data-driven insights. Therefore, my investment strategies are built upon the evidence discovered through a careful exploratory data analysis of the dataset - examining industry co-movements, liquidity effects, volatility patterns, and macroeconomic influences on returns. Through this process, I aimed to uncover what truly drives stock performance and how an investor can make smarter, more informed portfolio decisions.

To conduct this analysis, I first selected six major industry sectors - Tech, Consumer Retail, Financial Services, Health, Energy & Materials, and Industrial Manufacturing. For each stock, I retrieved five years of daily data (Open, High, Low, Close, Volume) from Yahoo Finance using the yfinance. After cleaning and standardizing the data, I chose three years to analyze and computed key indicators including Daily Return, Volatility (50-day rolling standard deviation), Volume Ratio, and Daily Range Percentage to capture both price dynamics and liquidity conditions. Next, I integrated macroeconomic factors from the Federal Reserve Economic Data (FRED) API, including the Ten-Year Treasury Rate, Federal Funds Rate, Consumer Price Index, and Consumer Sentiment Index. These were resampled to a daily frequency and forward-filled to align with stock-level data. I then merged the two datasets to evaluate how macro trends interact with sector-level returns.

Using correlation analysis, rolling window correlations, and heatmaps, I explored the interdependence among sectors and their time-varying relationships with macro variables. Additionally, I used Bokeh for interactive visualization to observe turning points and structural shifts over time, and Seaborn/Matplotlib for static statistical summaries. Overall, this methodology combines rigorous data preprocessing, and both static and interactive visualization techniques to uncover hidden interconnections among industries, reveal the temporal stability of correlations, and quantify the influence of macroeconomic forces on sector performance.

After completing the data collection, cleaning, and integration process, I began the exploratory analysis to answer a series of key questions derived from my initial motivation. Each question aims to uncover a specific dimension of the stock market dynamics - from how industries move together, to how liquidity impacts volatility, and finally, how macroeconomic forces shape sector returns. By addressing these questions one by one, I sought to build a comprehensive understanding of market behavior that could inform better investing strategies.

***Q1: Do Industries Move in Harmony - or Does Market Rhythm Differ Across Sectors?***

The first question I sought to answer was: “Do Industries Move in Harmony - or Does Market Rhythm Differ Across Sectors?” This question explores whether industries exhibit synchronized market behavior, and what this says about diversification potential. To investigate this, I calculated the average daily return of each sector and visualized their pairwise correlations using a heatmap.

<img width="909" height="761" alt="Screenshot 2025-10-23 at 17 45 30" src="https://github.com/user-attachments/assets/8f64d60b-3ba1-463a-8643-a588f05203dc" />

The color intensity clearly indicates the strength of relationships - darker shades represent stronger co-movements. Through this analysis, it became apparent that certain sectors, such as Financial Services and Industrial Manufacturing, tend to move closely together, while others, such as Health and Tech, exhibit relatively weak correlations. This asymmetry in correlation suggests that diversification benefits still exist across industries: investors who combine highly cyclical sectors (e.g., Financials, Industrials) with defensive or innovation-driven ones (e.g., Health, Tech) can meaningfully reduce portfolio volatility. In other words, the market does not move as a single rhythm but as an ensemble of distinct sectoral beats, allowing diversification to remain a powerful risk-management tool.


***Q2:Is Tech's Relationship with Other Sectors a Lasting Alliance or a Shifting Correlation?***

Having examined the overall co-movements among industries, I then turned my attention to one of the most dynamic and influential sectors in modern markets — the Tech sector. The next question I aimed to answer was: “ Is Tech's Relationship with Other Sectors a Lasting Alliance or a Shifting Correlation?”

To solve this question, I first drew some rolling correlation plots. Each plot shows the 60-day rolling correlation coefficient between Tech and another sector. Instead of computing a single static correlation, the rolling approach calculates the correlation within a moving 60-day window, allowing us to visualize how the relationship evolves dynamically through different market conditions. The red dashed line at 0 represents the threshold between positive and negative correlation - values above it indicate that the two sectors move in the same direction, while values below indicate they move oppositely. The green dotted line marks the average correlation level over the entire period. By including this line, we can quickly assess whether the relationship at a given time is stronger or weaker than its long-term average.

<img width="1628" height="849" alt="Screenshot 2025-10-23 at 17 46 15" src="https://github.com/user-attachments/assets/ef88e4f4-a07d-4b6d-a4ff-cc93eaf45077" />


One interesting thing I found is that these figures seem to have the same kind of shape. Thus, in order to see how similar they are, I create a plot that puts all these lines together. Additionally, I want to know what specific turning points (like the very bottom point in around 2024-08), so I create an interactive plot by using Bokeh.

[View Interactive Bokeh Plot](https://yyh2005201.github.io/Kelly-YU-s-midterm-project-for-NYU-Data-Bootcamp/bokeh_plot.html)

[Open Interactive html file)](bokeh_plot.html)


According to that plot, I found that while all industry pairs exhibit similar overall directional movements and common turning points, it is the significant disparity in their correlation coefficient ranges that proves most critical. This divergence underscores the dynamic and heterogeneous nature of inter-industry relationships, as certain pairs (like Tech vs. Consumer Retail), maintain a consistently high positive correlation, while others, such as Tech vs. Energy Materials, frequently traverse from positive to negative territory, offering substantially different diversification and hedging potential across market regimes.

***Q3: Does Trading Volume Amplify or Dampen Price Volatility? - When is the best time to invest?***

After exploring how industries move together, I wanted to understand what drives short-term price fluctuations - specifically, does trading activity amplify or stabilize volatility? In other words, when is the best time to invest?

<img width="796" height="573" alt="Screenshot 2025-10-23 at 17 47 07" src="https://github.com/user-attachments/assets/ddadf101-78fd-446e-aa33-ec57ac9d2c5c" />


To answer this, I examined the relationship between trading volume (liquidity) and price volatility across all sectors. Using each stock’s Volume Ratio - the ratio of daily trading volume to its 50-day moving average - I categorized market conditions into low, medium, and high liquidity periods. I then compared their corresponding Daily Range Percentages, which measure intraday price fluctuations. The results were quite intuitive yet revealing: there is a clear positive relationship between liquidity and volatility. Periods of higher trading volume tend to coincide with greater price swings, suggesting that active trading amplifies market fluctuations rather than stabilizing them. Conversely, low-volume periods tend to be calmer but may reflect slower information flow and less efficient price discovery. 

From an investment perspective, this insight implies that high-liquidity days are better suited for short-term trading strategies, where price momentum and rapid shifts can be exploited. In contrast, low-liquidity periods favor long-term investors seeking stability and gradual returns.

***Q4： Which macro factor contributes the most when explaining the changes in stock returns generally?***

Having understood how market liquidity affects volatility, the next step was to explore what external forces actually drive stock returns - in other words, which macroeconomic factors matter the most?

To investigate this, I integrated four key macro indicators from the Federal Reserve Economic Data (FRED): Ten-Year Treasury Rate (interest rate expectations), Federal Funds Rate (monetary policy stance), Consumer Price Index (CPI) (inflation pressure), and Consumer Sentiment Index (public confidence and spending outlook). By merging these indicators with sector-level daily returns, I calculated their correlations to determine which macro forces have the greatest influence on stock performance.

<img width="816" height="434" alt="Screenshot 2025-10-23 at 18 00 23" src="https://github.com/user-attachments/assets/ee3e37bd-f61a-410a-aafa-06fdcda428d6" />

The bar plot clearly shows in a ranking way that The Fed Fund Rate is identified as the "most influential macro factors", with an "intensity of influence" score of 0.025. This is followed by Consumer Price Index (CPI) at 0.017. Conversely, the Ten Year Rate (0.008) and Consumer Sentiment (0.007) have a significantly weaker impact, with Sentiment ranked as the "least influential".

This analysis demonstrates that while investor psychology makes headlines, it is fundamental economic variables, especially interest rates and inflation,  that truly move markets, which is not in line with my former thinking. Thus, for investors, this means paying attention to Federal Reserve policy decisions and inflation data can provide a more reliable foundation for timing and allocation strategies than sentiment-driven narratives.


***Q5： What are the relationships between macro factors and stocks from different industries?***

<img width="1321" height="841" alt="Screenshot 2025-10-23 at 18 00 54" src="https://github.com/user-attachments/assets/169800d6-13a4-44cb-9c7e-12f8a12ce05c" />

Nonetheless, while the overall analysis shows that some macro factors, like Sentiment, appear to have only a weak relationship with stock returns, this relationship is far from uniform across industries. In fact, when we break down the analysis by sector, a more nuanced picture emerges. For instance, the Fed Fund Rate, while impactful overall, is shown here to be the single most dominant factor for the Tech sector, with a sensitivity score of 0.055. In contrast, the Financial Service sector shows the broadest sensitivity, ranking as the "Most sensitive sector" for three of the four factors: TenYearRate (0.049), CPI (0.051), and Sentiment (0.034). This detailed view also identifies defensive sectors, such as Health, which is the "least sensitive" to both CPI and the Fed Fund Rate.(I listed the most sensitive and least sensitive sector directly below the plot.)
Additionally, this sector-specific sensitivity analysis allows an investor to move from general market observation to precise portfolio construction and risk management. An investor can now see exactly where macro risk is concentrated in their holdings; a portfolio heavily weighted in Tech and Financial Service stocks, for example, is exceptionally vulnerable to surprises in inflation and interest rate policy. Conversely, an investor seeking to build a defensive portfolio could overweight sectors like Health, which this data identifies as being the most insulated from those same factors. This analysis also helps filter market noise; it suggests a Tech investor can largely disregard "Sentiment" (the sector's least sensitive factor at 0.004) and focus instead on what truly matters to their holdings: the Fed Fund Rate.

**Conclusion：**

Based on the analysis above, the optimal investing strategy is not fixed, but rather depends on what type of investor you are. The data clearly show that market behavior changes with both liquidity and macroeconomic conditions — meaning that different investors can benefit under different regimes. For conservative or long-term investors, stability and risk control should come first. They can benefit from investing during low-liquidity periods, when volatility is subdued and prices are less reactive to short-term noise. In such times, focusing on defensive sectors like Health or Consumer Retail, and maintaining a diversified portfolio with some hedging positions, helps preserve value and reduce exposure to sudden macro shocks. For short-term or aggressive investors, higher volatility can actually mean greater opportunity. During high-liquidity phases, when trading activity and price swings both increase, there is potential to capture excess short-term returns through active trading or sector rotation — especially within rate-sensitive sectors such as Tech or Financial Services. However, these strategies require close monitoring of macro factors like the Fed Funds Rate and CPI, which this analysis has shown to be the most influential drivers of market movements. (or other factors that have not been analyzed)
In conclusion, there is no single “best” investment strategy — the optimal approach depends on each investor’s time horizon, risk tolerance, and reaction to changing market conditions. However, we can still derive several key insights from this data analysis. The findings suggest that investors should adopt a dynamic, data-driven approach — diversifying across sectors with different macro sensitivities, adjusting exposure according to liquidity conditions, and focusing on economic fundamentals rather than media-driven sentiment. By following these principles, investors can better navigate volatility, balance risk and return, and make more informed, evidence-based investment decisions.

