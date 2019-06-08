#include <stdio.h>
#include <stdbool.h> 
#define MAX_PICTURES 100 /*Change to increase or decrease the maximum capactity of the pictures that need to be recognized with a unique ID*/ 

/*Definition of Pixel */ 
typedef struct 
{
  unsigned char R; /* The value of the red component */ 
  unsigned char G; /* The value of the green component */ 
  unsigned char B; /* The value of the blue component */ 
} Pixel;

/*Definition of Picture */ 
typedef struct 
{
  int height; /* The actual height of the image*/
  int width;  /* The actual width of the image*/
  Pixel pix_array[266][427]; /* The array of pixels comprising the image */
} Picture;

/*Function Declarations*/ 

/*Functions to provide unique ID to each picture*/ 
float IdentifyPicture (Picture myPic, float myPictures [MAX_PICTURES]); 
/*Function to input the picture*/ 
Picture inputPicture (void); 

/*Provide unique ID to each picture */ 
float 
IdentifyPicture (Picture myPic, float myPictures [MAX_PICTURES])
{
  int RedSum = 0; /*Seperating for each sum in order to ease the future expansion of the algorithm */
  int GreenSum = 0; 
  int BlueSum = 0; 
  float uniqueID = 0; 
  bool repeated = false;  /*Is the PictureID repeated?*/ 
 
 
  /*Sum of each component of pixel*/ 
  for (int row = 0; row < myPic.height; row++){
    for (int col = 0; col < myPic.width; col++)
    {
    RedSum = RedSum + (myPic.pix_array[row][col]).R; 
    GreenSum = GreenSum + (myPic.pix_array[row][col]).G; 
    BlueSum = BlueSum + (myPic.pix_array[row][col]).B; 
   }//for 
  }//for 
  uniqueID = (RedSum + GreenSum + BlueSum) / 1000; 
  
  /*Handle repeated IDs */ 
 int pic = 0; 
 while ((pic <= MAX_PICTURES) && (repeated == false))
 {
     if (myPictures[pic]  == uniqueID)
     {
     uniqueID = uniqueID + 1; 
     repeated = true; 
     }
     else 
     pic++; 
 }
   return uniqueID;
}

Picture inputPicture (void)
{
   Picture currentPic; 
   /*************Store the taken picture in currentPic through some mechanism*******/ 
   /* I can do this for MyroC robots; however, I am unsure about the input that will be used here */ 
   return currentPic; 
}//input picture 


int main (void)
{
float picturesID[MAX_PICTURES]; /*Array to store the uniqueID of the pictures*/ 
int currentNumberOfPictures = 0; 
int continue_indetification = 1; 
printf ("Your first picture is being uniquely identified.\n"); 
while (continue_indetification)
{
Picture pic = inputPicture(); 
if (currentNumberOfPictures <= MAX_PICTURES)
{
picturesID[currentNumberOfPictures] = IdentifyPicture(pic, picturesID); 
currentNumberOfPictures++;
printf ("Now, do you want another picture to be uniquely identified? \n Press 1 to continue. \n Press 0 to quit. \n");
scanf ("%d", &continue_indetification); 
}//if 
else 
{
printf ("Maximum Capacity Exceeded. No more picturesID can be stored.\n"); 
continue_indetification = 0; 
}//else
}//while 
return 0; 
}//main 


