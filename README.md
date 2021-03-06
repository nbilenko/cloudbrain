![x](https://raw.githubusercontent.com/marionleborgne/cloudbrain/master/cloudbrain/webapp/static/images/cb-logo-low-res.png)

##Overview
CloudBrain is a platform for real-time EEG data analysis and visualization. [EEG](http://en.wikipedia.org/wiki/Electroencephalography) is the recording of electrical activity along the scalp. In other words, brainwaves.
<br>
<br>
CloudBrain enables you to:
- **Stream EEG data** into a central database.
- **Analyze EEG data** by computing aggregates.
- **Visualize EEG data** and patterns in real-time.

![x](https://raw.githubusercontent.com/marionleborgne/cloudbrain/master/cloudbrain-building-blocks.png)


## CloudBrain @ [The Exploratorium](http://www.exploratorium.edu) of San Francisco
CloudBrain is currently in use at the Exploratorium as part of the Exhibit called [*Cognitive Technologies*](http://www.exploratorium.edu/press-office/press-releases/new-exhibition-understanding-influencing-brain-activity-opens). All the EEG headsets in the exhibit are sending data to CloudBrain. This data is being routed to booths where visitors can control different things with their brain. For visitors who are willing to share their data, CloudBrain computes aggregates and displays a baseline of the average brain. On the central screen, visitors can see everyone else's live EEG data. Each radar chart shows the state of the main brainwaves (alpha, beta, theta, gamma, delta). This is particularly interesting to see how one's brain compares to others, or to understand how it reacts to different stimuli.

## Visualizations

### Aggregated data (bar charts)
![x](https://raw.githubusercontent.com/marionleborgne/cloudbrain/master/data-aggregates.png)

### Live EEG data (radar charts)
![x](https://raw.githubusercontent.com/marionleborgne/cloudbrain/master/radar-charts.png)

### Live EEG data (line charts)
![x](https://raw.githubusercontent.com/marionleborgne/cloudbrain/master/timeserie-data.png)

##Getting started with CloudBrain
- An instance of CloudBrain is currently running at `cloudbrain.rocks`.
- The packages that you want to use are `connectors` and `listeners`. Connectors will allow you to send live data to CloudBrain. Listeners will allow you to read live data from CloudBrain.
- Routing of live data is done via SpaceBrew (currently running on the CloudBrain server). To visualize how the data is being routed you can go to [this interface](http://spacebrew.github.io/spacebrew/admin/admin.html?server=cloudbrain.rocks).

##CloudBrain's Architecture
- `connectors`: connectors for [OpenBCI](http://openbci.com), [Muse](http://www.choosemuse.com/), [Neurosky](http://neurosky.com/) and [Spacebrew](https://github.com/Spacebrew/spacebrew) sending data to CloudBrain
- `listeners`: CloudBrain Listeners to get the live data data for [OpenBCI](http://openbci.com),[Muse](http://www.choosemuse.com/), [Neurosky](http://neurosky.com/) and [Spacebrew](https://github.com/Spacebrew/spacebrew)
- `webapp`: contains the UI & web API to retrieve the history of data, route live data, or retrieve data aggregated data (see [cloudbrain.rocks/api](http://cloudbrain.rocks/api) for the API documentation)
- `router`: router to update spacebrew routes (for the [Exploratorium](http://www.exploratorium.edu/) exhibition)
- `spacebrew`: python websocket wrapper to interface with [Spacebrew](https://github.com/Spacebrew/spacebrew)
- `database` : python wrapper to read and write data to cassandra

##Sending data to CloudBrain
- Install the [MuseIO SDK](http://www.choosemuse.com/developer-kit/)
- Pair your Muse via Bluetooth.
- Start MuseIO: open a terminal or command prompt and run: `muse-io --osc osc.udp://localhost:9090`
- Open a new terminal tab and run:
<br>
`git clone https://github.com/marionleborgne/cloudbrain`
<br>
`cd cloudbrain/connectors/spacebrew`
<br>
`pip install websocket-client`
`python spacebrew_server.py --name=YOUR_NAME_HERE`
- The last command will register your muse to CloudBrain's Spacebrew
- Check if you muse is in the column “publishers” of the [SpaceBrew interface](http://spacebrew.github.io/spacebrew/admin/admin.html?server=cloudbrain.rocks).

##Reading data from CloudBrain
- Open a new terminal tab and run:
<br>
`cd cloudbrain/listeners`
<br>
`python example_spacebrew_client.py --name=YOUR_NAME_HERE`
- The last command will register your booth to cloudbrain’s spacebrew
- Check if you booth is in the column “subscridbers” of the [SpaceBrew interface](http://spacebrew.github.io/spacebrew/admin/admin.html?server=cloudbrain.rocks).

## Infrastructure @ [The Exploratorium](http://www.exploratorium.edu/)
![x](https://raw.githubusercontent.com/marionleborgne/cloudbrain/master/exploratorium-exhibit-overview.png)

Infrastructure v2.0 
![x](https://raw.githubusercontent.com/marionleborgne/cloudbrain/master/infra.png)
