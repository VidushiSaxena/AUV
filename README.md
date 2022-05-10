//main 1
#include <opencv2/highgui.hpp>
#include<opencv2/imgcodecs.hpp>
#include<opencv2/imgproc.hpp>
#include <iostream>

using namespace std;
using namespace cv;

int main()
{ Mat imgHSV,mask;
int hmin=78,smin=176,vmin=125;
int hmax=82,smax=217,vmax=138;
 string path="/home/vidushi/cpp_auv/sample2.jpeg";
 Mat img = imread(path);
cvtColor(img,imgHSV,COLOR_BGR2HSV);
namedWindow("Trackbars",(250,640));
createTrackbar("Hue Min","Trackbars",&hmin,179);
createTrackbar("Hue Max","Trackbars",&hmax,179);
createTrackbar("Sat Min","Trackbars",&smin,255);
createTrackbar("Sat Max","Trackbars",&smax,255);
createTrackbar("Val Min","Trackbars",&vmin,255);
createTrackbar("Val Max","Trackbars",&vmax,255);

while(true)
{
Scalar lower(hmin,smin,vmin);
Scalar upper(hmax,smax,vmax);
 inRange(imgHSV,lower,upper,mask);
 imshow("Image",img);
 imshow("Image hsv",imgHSV);
 imshow("Image mask",mask);
 waitKey(1);
}
 return 0;
}

  
  
  
  //main 2
  #include <opencv2/highgui.hpp>
#include<opencv2/imgcodecs.hpp>
#include<opencv2/imgproc.hpp>
#include <iostream>

using namespace std;
using namespace cv;
 
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>
#include <opencv2/imgproc.hpp>
#include <iostream>
 
using namespace cv;
using namespace std;
 
 
void getContours(Mat imgDil, Mat img) {
 
	vector<vector<Point>> contours;
	vector<Vec4i> hierarchy;
 
	findContours(imgDil, contours, hierarchy, RETR_EXTERNAL, CHAIN_APPROX_SIMPLE);
	vector<vector<Point>> conPoly(contours.size());
	vector<Rect> boundRect(contours.size());

	for (int i = 0; i < contours.size(); i++)
	{
		int area = contourArea(contours[i]);
		//cout << area << endl;
		string objectType;
 
              	float peri = arcLength(contours[i], true);
			 approxPolyDP(contours[i], conPoly[i], 0.0002 * peri, true);
			//cout << conPoly[i].size() << endl;
			boundRect[i] = boundingRect(conPoly[i]);
                    
			drawContours(img, conPoly, i, Scalar(255, 0, 255), 2);
			rectangle(img, boundRect[i].tl(),boundRect[i].br(), Scalar(0, 255, 0), 2);
	
	}
             cout<<(float)boundRect[3].height<<endl;
}



int main()
{ 

Mat imgHSV,mask;
int hmin=0,smin=185,vmin=21;
int hmax=29,smax=255,vmax=93;
 string path="Resources/sample2.jpeg";
 Mat img = imread(path);
cvtColor(img,imgHSV,COLOR_BGR2HSV);
 Mat imgGray;
Scalar lower(hmin,smin,vmin);
Scalar upper(hmax,smax,vmax);
 inRange(imgHSV,lower,upper,mask);
Mat imgBlur,imgCanny,imgDil;
  cvtColor(img,imgGray,COLOR_BGR2GRAY);
  GaussianBlur(imgGray,imgBlur,Size(3,3),3,0);
  Canny(imgBlur,imgCanny,25,75);

Mat kernel = getStructuringElement(MORPH_RECT,Size(3,3));
dilate(imgCanny,imgDil,kernel);

getContours(mask,img);

imshow("Image",img);
/*
imshow("Image Gray",imgGray);
imshow("Image Blur",imgBlur);
imshow("Image Canny",imgCanny);
imshow("Image Dilation",imgDil);
*/
waitKey(0);
 return 0;
}
                                                    

                                                    
 //main3
 #include <opencv2/highgui.hpp>
#include<opencv2/imgcodecs.hpp>
#include<opencv2/imgproc.hpp>
#include <iostream>

using namespace std;
using namespace cv;
 
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>
#include <opencv2/imgproc.hpp>
#include <iostream>
 
using namespace cv;
using namespace std;
 
 
void getContours(Mat imgDil, Mat img) {
 
	vector<vector<Point>> contours;
	vector<Vec4i> hierarchy;
 
	findContours(imgDil, contours, hierarchy, RETR_EXTERNAL, CHAIN_APPROX_SIMPLE);
	vector<vector<Point>> conPoly(contours.size());
	vector<Rect> boundRect(contours.size());

	for (int i = 0; i < contours.size(); i++)
	{
		int area = contourArea(contours[i]);
		//cout << area << endl;
		string objectType;
 
              	float peri = arcLength(contours[i], true);
			 approxPolyDP(contours[i], conPoly[i], 0.0002 * peri, true);
			//cout << conPoly[i].size() << endl;
			boundRect[i] = boundingRect(conPoly[i]);
                    
			drawContours(img, conPoly, i, Scalar(255, 0, 255), 2);
			rectangle(img, boundRect[i].tl(),boundRect[i].br(), Scalar(0, 255, 0), 2);
	
	}
             cout<<(float)boundRect[3].height<<endl;
}



int main()
{ 

Mat imgHSV,mask;
int hmin=0,smin=185,vmin=21;
int hmax=29,smax=255,vmax=93;
 string path="/home/vidushi/cpp_auv/sample2.jpeg";
 Mat img = imread(path);
cvtColor(img,imgHSV,COLOR_BGR2HSV);
 Mat imgGray;
Scalar lower(hmin,smin,vmin);
Scalar upper(hmax,smax,vmax);
 inRange(imgHSV,lower,upper,mask);
Mat imgBlur,imgCanny,imgDil;
  cvtColor(img,imgGray,COLOR_BGR2GRAY);
  GaussianBlur(imgGray,imgBlur,Size(3,3),3,0);
  Canny(imgBlur,imgCanny,25,75);

Mat kernel = getStructuringElement(MORPH_RECT,Size(3,3));
dilate(imgCanny,imgDil,kernel);

getContours(mask,img);

imshow("Image",img);
/*
imshow("Image Gray",imgGray);
imshow("Image Blur",imgBlur);
imshow("Image Canny",imgCanny);
imshow("Image Dilation",imgDil);
*/
waitKey(0);
 return 0;
}
