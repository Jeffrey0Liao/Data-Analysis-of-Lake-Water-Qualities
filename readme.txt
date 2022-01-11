***** This readme file describes how Task-1 & Task-2 are done for 2020 COMP 3055 coursework*****



General description:

The data chosen in this coursework comes from the China Lake. Rudimentary data
preprocessing is leveraged with Pandas library. Firstly, by filtering data with their
features, we found that most data are collected at depth of 7, station 1. Therefore, data
does not match these criteria is deprecated. Secondly, after filtering, valid data of CHLA,
Temperature, and Total P apparently overlaps in the period from 1998 to 2013.
Therefore, only data within this period is kept for further analysis. 



How to run the code:

	* All source code is in COMP3055-Code-20030694.ipynb.
	* Please use 'China Lake. xlsx' along in the coursework folder, some names of columns are changed for simplicity.
	* Put the excel file and the ipynb file under the same directory
	* run the code.



Task-1:

The first method is mean value method.
	1. Daily data are filtered, tuples are droped if it contains any NaN value. Droped tuples are kept. 
	2. Data are thus splited into two halves: full daily data (P1), and unfull daily data (P2).
	3. Use a month selector to aggregate P1 into monthly data (if multiple full tuples exist for a single month, averages are used). 
	4. For missing months, find back into P2 and see if any value could be used here. 
	5. For data which is still missing, average value inference is applied: 
		5.1. If there is less than two avaiable values for any of the features in one year, we drop the whole year. 
		5.2. Otherwise, we use the relationship of: (month1+month2)/2 = month3 to infer any of the missing values based on the given ones (note that if month1 and month3 are given we could also derive month2 based on the relationship). 

The second method is linear interpolation.
	We start from the end of step 4 in the first method:
	5. For data which is still missing, linear interpolation is applied:
		5.1. For any segment of missing data, we determine the two nearest valid points to the head and the tail of it.
		5.2. We draw a line between the two points in the form of y=kx+b.
		5.3. Since all x values are known, we use it to estimate y.
	6. For data which is still missing, extrapolation is applied:
		6.1. For the segment of missing data whose two nearest valid points to the head and the tail could not be determined i.e. the missing data starts from the first row, we instead find several nearest points from one edge of it. 
		6.2. We regress a line using these points.
		6.3. Since all x values are known, we use it to estimate y.



Task-2:

1. Pearson correlation coefficient:
	* Function: DataFrame.corr(method='Pearson') is used to calculate the matrix.
	* Function: DataFrame.rank() is used to rank correlation coefficients

2. Spearman correlation coefficient:
	* Function: DataFrame.corr(method='Spearman') is used to calculate the matrix.
	* Function: DataFrame.rank() is used to rank correlation coefficients

3. Kendall correlation coefficient:
	* Function: DataFrame.corr(method='Kendall') is used to calculate the matrix.
	* Function: DataFrame.rank() is used to rank correlation coefficients

4. Biweighted midcorrelation:
	* Function: scipy.spatial.distance.correlation(feature1, feature2) is used to calculate the relavence.
	* Dictionary structure are set up to store coefficients
	* Dictionary structure are tranformed to DataFrame structure
	* Function: DataFrame.rank() is used to rank correlation coefficients

5. Maximal information coefficient:
	* mingpy.MINE() are instantiated as mine.
	* Function: mine.compute_score() are used to calculate the relavence.
	* Function: mine.mic() are used to extract maximal information coefficients
	* Dictionary structure are set up to store coefficients
	* Dictionary structure are tranformed to DataFrame structure
	* Function: DataFrame.rank() is used to rank correlation coefficients