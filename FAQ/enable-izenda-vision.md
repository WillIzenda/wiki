#Enable Izenda Vision & HTML Charting

**To Enable HTML Charting**

- Set ``AdHocSettings.ChartingEngine = ChartingEngine.HtmlChart;`` - typically inside your _global.asax_.

- Create sample reports.

**To Enable VISION**

Izenda Vision is a rich extension to the API to include many cutting-edge data visualizations to your Izenda-enabled application. Here are the steps required to start using Izenda Vision.

- Purchase a Vision License.

- Set a key with +VISION included within your deployment, typically within the _global.asax_.

- Add the /vis directory to your /Resources directory if it is not already there.

- Set ``AdHocSettings.ChartingEngine = ChartingEngine.HtmlChart;`` - typically inside your _global.asax_.

- Create sample reports.

- You can now copy and customize existing visualizations from inside the **/vis** folder, or add your own.