# handwritten_digit_reader
Introduction

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The scope of this project is to develop an algorithm that will successfully generate a barcode and search images in a given dataset.  The algorithm should be designed for a large dataset such as the given MNIST dataset, which contains 100 handwritten digits (originally 70,000).  Ideally, the purpose of this program is to find the closest image that is part of its class, excluding the image that is being searched.  Our goal is to construct a quick and reliable content-based image retrieval algorithm that can outperform the Radon based method.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;We can split our overall system into two algorithmic programs named Barcode_Generator and Search_Algorithm.  The Barcode Generator will do exactly what it is named, that is to create a barcode for an image in the dataset, and the Search Algorithm will have to search a query image in the dataset. 

Algorithms

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The main function of our Barcode_Generator algorithm is to convert an image into a matrix and create a unique barcode from that.  This can be achieved through Python’s Imaging Library Pillow, which can read and convert a single image pixel into a numeric value that determines the colour.  Exhaustively, this has to be done for every single pixel in the image, for all images in the dataset.  This data is then stored in a 3-dimensional array, with each image index pointing to its 2-dimensional matrix, containing the converted pixel values.  The first main step is now completed, and we are now able to work with the raw data from the given dataset. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The second step requires the algorithm to calculate directional projections from the raw data.  Our team has decided to calculate three projections, mainly the row, column and diagonal projections from the raw data.  Each projection functions the same, where the sums of the directional projections are stored in seperate 2-dimensional arrays, always keeping track of the images index.  We now have three separate arrays that store the sums of the three different direction projections.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The third step converts the directional projections into binary, also known as a barcode.  Using the directional projection arrays, we make three more arrays that correspond to each directional projection.  The barcode conversion method creates an average of every sum in the projection, and compares that average to a given threshold.  If the calculated threshold is greater than or equal to the given threshold, we insert a 1 into the array, otherwise it inserts a 0.  We are now left with a barcode for each directional projection for each image, now we must parse these three directional barcodes to make a single barcode.  Each image now has an 84 digit barcode with 1’s and 0’s, all stored in a 2-dimensional array.   

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The second algorithm includes the barcode search function, which will ideally compare all 100 image barcodes with one another.  Taking into consideration that a tested image cannot return itself, the goal is to return a picture that is in the same class.  The compare method compares 1 barcode to 99 different barcodes, and counts the number of correct digits in each different barcode, which is then stored into a temporary array (hamming distance).  We then use a function to find the index of the max value in this temporary array, and store that index into our Best_image array, which we will use later to calculate the hit ratio and print the results.  This method is called for the remaining 99 images which follows the same procedure.  Through this we have an array that holds the indexes of the best image found that closely resembles the tested (actual) image.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Our group has also added a function to display the image results and shows all 100 images and the closest image that it resembles.  The display function splits the data into two columns, the tested images and the found images, and plots the actual images through Python’s Matplotlib library.  Our group took advantage of the fact that the images were already in folders named 0 - 9, which resembles the image classes, and the images itself could be renamed also using digits 0 - 9.  We utilized this and through simple math, we can use for loops to display images starting from 0 to 100 accordingly with the Best_Image array, which will output the closest image.  
Measurements & Analysis 

![search_results](https://user-images.githubusercontent.com/77807505/135936378-a1165b7d-e7b7-4f9b-9d0a-53f078cb008b.png)


Search Results

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Utilizing our search algorithm, we have an array that tells us the best image found in comparison to the actual image.  Since we have renamed all images using digits from 0 to 9, and those images were already in their respected numbered class folder, we could find and compare the tested image class with the resulting image class.  The rest is simple as whenever the classes equaled the same number, the success counter would increase.  This would determine our hit ratio, with 40 out of 100 images that belonged in the same class. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Given our 40% accuracy, there is plenty of room for improving our program to result in higher accuracy.  Two examples include increasing the number of projections taken and calculating a more efficient threshold value, which will definitely return a higher hit ratio.  The diagonal projection could also have been more efficiently produced, as only the single main diagonal was recorded instead of taking 28 different diagonals, which was taken with the row and column projections.  This choice resulted in a less complicated algorithm and Big-o complexity for the diagonal projection.  A better and more careful threshold value would naturally arise as the barcode length would increase with projections. 

Sample output:

![sample](https://user-images.githubusercontent.com/77807505/135936450-d6b4ba63-67e6-4b22-ab92-03a502d84739.png)

Conclusion

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Throughout this project we were successfully able to expand our knowledge of real life applications for algorithms. We were able to design a successful algorithm to accept large data sets and compute to find the closest result to the original given data. We designed a barcode generator and a search algorithm to compute the data. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Our algorithm’s accuracy is fairly low at 40% but being our first large data set algorithm we are fairly satisfied with the results with lots of possible improvements in the future. Designing a much more complex algorithm would result in a higher accuracy but to develop that would have taken a lot more practice and time. With the algorithm being less complex this has resulted in quick retrieval times where adding more projections would cause the overall time to increase. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This project really put our knowledge of algorithms to the test and allowed us to learn the deeper understandings of algorithms with real life applications. We weren’t able to develop an algorithm more accurate than Radon Barcode (RBC) but we can still take a lot from this experience and learning development. As software engineering students this will help in our future experience with more complex algorithms and we look forward to upcoming courses in this field.
