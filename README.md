# Modlines Database
## About
This is just a "list" of modlines for the X.org Display Server.

In this list you will find modlines compiled for the monitors factory specifications and as well modelines that pust the limits, for instance, displaying resolutions of 1152x900 and even 1280x960 on 1024x768 VGA LCDs.

## Factory Specifications
When I say *factory specification* I mean things like.

* Min and max horizonal and vertical sync frequencies.
* Min and max dot/pixel clock frequency.
* Officially supported resolutions.
* Native LCD panel resolution.

### Finding the factory specifications/monitor specifications
#### On the web
All these information can be found on the web.

Simply search for +"Brand" +"Model"
+"Service Manual". For example, for my HP L1506 I serched for +"HP" +"L1506" +"Service Manual".

#### Command line
You can use the command **edid-decode** to read such specifications straight from your monitor. Refer to *Reference.md* for more information.

## Factory vs Overclock
### Factory
The **Factory** definition should only include modlines that respect all factory specifications.

### Overclock
With this definition you will find modelines that will *"overclock"* your monitor, with higher resolutions or frequency that it is supposed to go. **It may damage you display adapter and monitor.**

## Repository Structure
The repo is orgnized as it follows.

In the folder **Modelines** You will find a folder for each **brand** and in each brand folder a folder per **display model**. In the display model folder you find files following the naming convention "*Brand*-*MonitorModel*-*ModelCode*(Optional)-*factory*-Modelines.txt" for factory specifications and "*Brand*-*MonitorModel*-*ModelCode*(Optional)-Overclock*-Modelines.txt" for when we want to push the limits.

### Example
HP-L1506-T560KC4DKHHPNP-Factory-Modelines.txt
HP-L1506-T560KC4DKHHPNP-Overclock-Modelines.txt

Samsung-SF354-LS24F354FHNXZA-Factory-Modelines.txt
SONY-Bravia-FWD-32WE615-Factory-Modelines.txt
