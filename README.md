RecDistCalc
===========

Calculate rectangular distance of GPS coordinates, please!

#include <TinyGPS++.h>
/* 
   Author: Matt Pistacchio
   Date: 4/30/14
   Program: RecDistCalc.ino
   
   Purpose: input two sets of lat and lon, and output rectangular
   distance in serial port
*/

// A sample NMEA stream to be used to apply a logic truth

const char *gpsStream =
  "$GPRMC,045103.000,A,3014.1984,N,09749.2872,W,0.67,161.46,030913,,,A*7C\r\n"
  "$GPGGA,045104.000,3014.1985,N,09749.2873,W,1,09,1.2,211.6,M,-22.5,M,,0000*62\r\n"
  "$GPRMC,045200.000,A,3014.3820,N,09748.9514,W,36.88,65.02,030913,,,A*77\r\n"
  "$GPGGA,045201.000,3014.3864,N,09748.9411,W,1,10,1.2,200.8,M,-22.5,M,,0000*6C\r\n"
  "$GPRMC,045251.000,A,3014.4275,N,09749.0626,W,0.51,217.94,030913,,,A*7D\r\n"
  "$GPGGA,045252.000,3014.4273,N,09749.0628,W,1,09,1.3,206.9,M,-22.5,M,,0000*6F\r\n";

// The TinyGPS++ object
TinyGPSPlus gps;
//"inputs"
const double lat1 = 42.75115;	
const double lon1 = -73.63021;
const double lat2 = 42.74581;
const double lon2 = -73.64158;
double distance = gps.distanceBetween(lat1,lon1,lat2,lon2);

void setup()
{
  Serial.begin(115200);
  while (*gpsStream)
    if (gps.encode(*gpsStream++))
      
      Serial.println(distance,6); 
      // ^ print rec dist to six digits after decimal point
}

void loop()
{
}
/////////////////////////////////Fin//////////////////////////////
