This reading item contains a collection of common chart types along with a description, strengths, weaknesses, typical data, and examples for each. You can come back here any time if you want to get some inspiration for visualizing your data. There are many more ways of making visualizations, but this item contains a general overview of the most commonly used types.

## Bar and column chart

A bar chart is a graphical representation of data that uses rectangular bars to show the frequency or value of different categories. Each bar's length is proportional to the data it represents, making it easy to compare different categories at a glance. Bar charts can be displayed vertically or horizontally, depending on the data and the desired visual effect. They are commonly used to compare numerical outcomes across different categories, such as sales figures for different types of items or for different quarters, survey responses, or any other categorical data, providing a clear and straightforward way to visualize and interpret information.

A column chart is just another name for the bar charts with vertical bars.

### Pros:

- Compare quantities across different categories, highlighting differences clearly.
- Can be used to display both positive and negative values, which is useful for showing profit and loss, for example.

### Things to look out for:

- Bar charts can become cluttered and hard to read if there are too many categories.
- They are not suitable for showing trends over time, which often have too many data points - in this case a line chart is better. However when you have only a few data points such as a few months, they can be suitable.

### Data commonly visualized using this chart type:

- Number of products sold in different regions.
- Survey responses by option (e.g., favorite fruit).
- Population by age group
- Website traffic by source
- Employee count by department
- Survey responses by option

### Example column chart:

![[column-chart-example.png]]

### Example bar chart:

![[bar-chart-example.png]]
## Grouped bar chart

A grouped bar chart, also known as a clustered bar chart, displays multiple bars for each category, representing different sub-categories or groups. This type of chart is useful for comparing multiple series of data across the same categories.

### Pros:

- Allows for direct comparison between different groups within the same category.

### Things to look out for:

- Can become cluttered with too many groups or categories.
- May require careful color-coding to distinguish between groups.

### Data commonly visualized using this chart type:

- Monthly sales data for different stores.
- Exam scores across different subjects for multiple classes.
- Quarterly sales revenue by product category
- AveragedDaily temperature by month for multiple cities

### Example:

![[grouped-bar-chart-example.png]]
## Stacked bar chart

A stacked bar chart displays bars divided into segments that represent sub-categories, stacked on top of each other. This type of chart is useful for showing the cumulative total and the contribution of each sub-category to the whole. It can also be normalized, so that all bars have the same height, to compare fractions of the total.

### Pros:

- Shows the cumulative total and the contribution of each sub-category.
- Efficient use of space, as multiple data series are stacked in a single bar.

### Things to look out for:

- Can be difficult to interpret individual segment sizes, especially if there are many segments.
- Difficult to compare individual sub-categories across different bars.

### Data commonly visualized using this chart type:

- Monthly sales data broken down by product categories.
- Budget allocation across different departments over time.

### Example:

![[Stacked-bar-chart-example.png]]
### Example (stacked bar chart displayed as a percentage of the total):

You can also create a stacked bar chart where each bar represents the percentage share of the total, so all the bars add up to the same height. This is useful when you want to detect relative differences. For this you need to normalize the data so that the sum of the segments in each bar equals 100%.

![[Stacked-bar-chart-percent-example.png]]
## Scatter plot

A scatter plot is a type of data visualization that displays individual data points on a two-dimensional graph. Each point represents the values of two variables, with one variable plotted along the x-axis and the other plotted along the y-axis. Scatter plots are useful for identifying relationships, correlations, and patterns between the two variables. They can reveal trends, clusters, outliers, and the overall spread of the data. Scatter plots are commonly used in statistical analysis, scientific research, and data exploration to visually assess the strength and direction of relationships between variables.

### Pros:

- Show relationships between two variables, revealing correlations, patterns, and outliers.
- Can display a large amount of data points.

### Things to look out for:

- Can be difficult to interpret when data points overlap.
- Not suitable for categorical data.

### Data commonly visualized using this chart type:

- Hours studied vs. exam scores
- Age vs. income
- Advertising spend vs. sales revenue
- Temperature vs. ice cream sales
- Height vs. weight of individuals.

### Example:

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/h94P12J7QuebZ1pCFCGr3w_9374c5c237ce44138a9dc389e4e7d8a1_AD_4nXcm7_or6twXi7qAJ8m01qZAlMlj9AYSYqi2UXGZFsVxHaCSB0k3nOIM8XNGh9aBu1lKEL0e-qUdpAbfypKDB99FBtdoe-9O3nXpoiByo5pa3IHbaeBlsdYg4pc1ptvwjJXkE_NCD4bOSaEzBYVjiP7Kif2G?expiry=1742601600000&hmac=OpLbhiRL2NZHlf4O_qTNLvOSLzwV0fZVYD_dvOUTb7s)

## Line chart

A line chart is a type of graph used to display information that changes over time. It consists of a series of data points indicated by markers connected by straight line segments. Each marker represents a value at a specific point in time, and the connected lines help to illustrate trends, patterns, and fluctuations in the data over the specified period. Line charts are particularly useful for visualizing time-series data, such as stock prices, temperature changes, or monthly sales figures. They provide a clear and straightforward way to observe the direction and magnitude of changes.

### Pros:

- Show trends over time, making them ideal for time series data.
- Display multiple data series for comparison, allowing for the observation of patterns and correlations.

### Things to look out for:

- Not suitable for categorical data.
- Can become cluttered and hard to read with too many lines.
- Use distinct colors or styles for different lines, and take into account color blindness

### Data commonly visualized using this chart type:

- Monthly sales revenue over a year
- Daily temperature changes over a week
- Stock prices over a month
- Website traffic over a year
- Annual population growth over a decade

### Example:

![[Line-chart-example.png]]
## Pie Chart

A pie chart is a circular graph used to display data in a way that shows the relative proportions of different categories within a whole. Each slice of the pie represents a category's contribution to the total, with the size of each slice being proportional to the category's value. Pie charts are particularly useful for visualizing percentage distributions and comparing parts of a whole. They provide an intuitive and visually appealing way to understand the composition of data.

### Pros:

- Pie charts are straightforward and can be quickly understood by most people, making them ideal for presenting simple data sets.
- They provide a visually engaging way to display proportions and are often used in presentations and reports.
- They are effective for Small Data Sets

### Things to Look Out For:

- Not Suitable for Large Data Sets
- Not suitable for showing data that does not add up to a whole
- It can be challenging to compare the sizes of slices accurately, especially when they are similar in size.
- Avoid 3D Effects: 3D pie charts can distort perception and make it harder to accurately judge the proportions.
- Use Distinct Colors: Ensure that each slice has a distinct color to avoid confusion, and consider color blindness when choosing colors.

### Data Commonly Visualized Using This Chart Type:

- Displaying the market share of different companies within an industry.
- Showing how a budget is distributed across different departments or categories.
- Visualizing the percentage distribution of responses to a survey question.
- Depicting how resources or time are allocated across various tasks or projects.

### Example:

![[pie-chart-example.png]]
## Conclusion

Each type of chart or plot has its unique strengths and is best suited for specific types of data and analytical needs. Choosing the right visualization depends on the nature of the data, the insights you aim to convey, and the audience's familiarity with different types of charts.

If you are interested in data visualizations beyond the charts you saw here, take a look at the additional optional reading item, which shows some more types of charts, or check out some of the books and further readings collected at the end of this course.