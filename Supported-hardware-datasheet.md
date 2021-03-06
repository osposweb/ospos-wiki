A standard OSPOS setup is comprised of a web server, a web browser client, a barcode reader, a cash drawer and a receipt printer.
OSPOS supports the following devices:

| Device  | Related information and documentation |
| ------------- | ------------- |
| Machine runtime | The hardware where OSPOS will run and server, could be any that runs php, mysql and the webserver. Inclusively can run in Android or RasberryPi hardware, please see [our Hardware requirements wiki page (click here)](OSPOS-development-index#requirements) |
| Machine usage | The hardware where OSPOS will be consume an use it, could be any that runs Firefox or any modern web browser; wiki info at [OSPOS Installation requirements (click here)](OSPOS-development-index#tech-installation), Works perfectly with Mobiles but a PC/MAC is recommended |
| Barcode scanners | Any barcode scanner will work as if programmed to hit return after scanning. We recommend a [Datalogic scanner](https://www.amazon.com/gp/search/ref=as_li_qf_sp_sr_tl?ie=UTF8&tag=ospos-20&keywords=datalogic%20quickscan&index=aps&camp=1789&creative=9325&linkCode=ur2&linkId=4278b9783c5aaad9dc17ae38debc6f3e) as they are easy to configure and well supported. Mobile barcode reading its not supported yet. |
| Printers  | Depends entirely of [the browser and OS](Printing). We recommend a [Star TSP 1431IU](https://www.amazon.com/gp/search/ref=as_li_qf_sp_sr_tl?ie=UTF8&tag=ospos-20&keywords=Star%20TSP143&index=aps&camp=1789&creative=9325&linkCode=ur2&linkId=68fb044e8a64e9842477d82710e8fd70) or [Epson TM-88VI](https://amzn.to/38XX2VL). If you consider buying one on Amazon then please use our referral links to contribute back to the project! |
| Cash drawers  | Can be handle by some printers, but the manage of the cash drawers currently this are out of the scope due the system are web based.  |
| Credit Card Reader | Not suported. Currently there's no plans to work on. |
| Digital Signature Capture | Not supported yet |
