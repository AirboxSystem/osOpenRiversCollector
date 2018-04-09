# osOpenRiversCollector
Process OS OpenRivers into a set of uniquely named GB watercourses.

The script is merely a stage in the processing of the dataset.

1. Download the OS OpenRivers Dataset from the [OS OpenData Download](https://www.ordnancesurvey.co.uk/opendatadownload/products.html) pages
2. Import the 'watercourselink' and 'hydronode' shapefiles into a postgres database
3. Change the script provided to suit your setup - depending on your setup you will likely need to change _schema, _nodes_table, _links_table and will possibly need to change _proc_table and _out_table
4. Connect to the database and run the script as an anonymous block (i.e. copy and paste the entire script provided)
5. Depending on your machine specification you may have time for a coffee, nap or a holiday until the script finishes
6. Export the data from the database in the format required

The script provides constant updates in the form of messages being printed to the console. Some steps require significantly more time than others, especially at the beginning. Unless the process running the script is hung up you can safely assume the script to still be running fine. On a i5-3320M, 16GB machine the processing takes around 22 hours when left to work over the weekend with no other use of the machine.

The script produces a clean and stripped down dataset containing only the named GB watercourses. Where multiple watercourses exist with the same name (e.g. River Avon) each unique river is provided with a unique identifier. The script does NOT geolocate these further than their contained geometry. the script does calculate the length within the database. This could be used to differentiate between different rivers of the same name if one is significantly longer than the other. The value is merely the combined length of all links in the geometry and as such is not 100% accurate.

At present this script only uses the name1 field of the data to determine streams and name these. This causes issues in Wales and Scotland where some streams are named under their Welsh and Gaelic names under name1 and only provide the English names under name2. This results in the River Severn only showing up under its Welsh name of Afon Hafren. The script is being changed to account for this, though in the meantime it could be run twice, once using name1 and once replacing all references to name1 with name2. This would result in two independent datasets of uniquely named streams.

The script automatically fills in unnamed gaps between named links starting from the source and working its way downstream to the outflow. There are some anomalies that need manual fixing, especially on the River Thames, Humber and Severn, though these may well disappear or change based on the input data currency.

The script is provided unsupported and as-is in line with the license, with no future public updates planned (except for multi name support). Commercial support options may be available on request.
