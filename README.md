# mdsj
MDSJ – Multidimensional Scaling for Java (clone of defunct project)

This repository is a copy of content that is no longer hosted at http://algo.uni-konstanz.de/software/mdsj/
skyebend is *not* the author of this package. 

MDSJ is a free Java library for Multidimensional Scaling (MDS).

It is a free, non-graphical, self-contained, lightweight implementation of basic MDS algorithms and intended to be used both as a standalone application and as a building block in Java based data analysis and visualization software.

It is developed at the University of Konstanz, Department of Computer & Information Science, Algorithmics Group. It is free for academic and research purposes; no registration is required. See the License Conditions below for the conditions of use.

Multidimensional Scaling is a family of methods for the geometric representation of data. It turns the information about the similarity of data objects into geometric positions in such a way that, hopefully, similar objects are close together and dissimilar objects are far apart.

Finding these geometric positions is useful for visualizing data that are intrinsically non-geometric, but among which (dis)similarity information is present or can be constructed. MDS has applications in manifold areas, such as psychology, computer graphics, statistics, data analysis etc.

More formally, there are n data objects 1,...,n. For each possible pair of i,j of these objects a nonnegative d(i,j) expresses how dissimilar the two objects i and j are. The resulting positions x1,...,xn should have Euclidean distance ||xi – xj|| that approximates the original dissimilarity d(i,j) as closely as possible.

Features

* Classical MDS in multiple dimensions
* Pivot MDS, an efficient MDS variant for very large data sets – see U. Brandes and C. Pich, Eigensolver Methods for Progressive Multidimensional Scaling of Large Data. Proc. 14th Intl. Symp. Graph Drawing (GD '06). LNCS 4372, pp. 42-53. © Springer-Verlag, 2007.
* Stress minimization (by the SMACOF majorization algorithm) with arbitrary weights and dimensions
* Stress minimization with rectangular dissimilarity matrices
* simple Java API, MDSJ as external Java library
* easy-to-use command line tool

Download

The current version is v0.2 [2009-11-18]. It does not depend on a specific operating system or platform, but merely requires a runtime environment of Java 1.5 or higher to be installed on your system.

* mdsj.jar – the MDSJ archive
* MDSJExample.java – an example Java file using MDSJ
* mdsj-doc.zip – Javadoc API Documentation
* Sample data: nations.txt, nations-cmds.txt
For detailed information on methods and background, see C. Pich, Applications of Multidimensional Scaling to Graph Drawing, PhD thesis, University of Konstanz, 2009.

Usage

The file mdsj.jar is required to be included on your classpath.

Usage as a class library: You can use all classes in the mdsj.* package in your own Java software.

Javadoc API Documentation
A sample Java class using MDSJ (MDSJExample.java).
```
import mdsj.MDSJ;

public class MDSJExample {
	public static void main(String[] args) {                                           
		double[][] input={        // input dissimilarity matrix
		    {0.00,2.04,1.92,2.35,2.06,2.12,2.27,2.34,2.57,2.43,1.90,2.41},
		    {2.04,0.00,2.10,2.00,2.23,2.04,2.38,2.36,2.23,2.36,2.57,2.34},
		    {1.92,2.10,0.00,1.95,2.21,2.23,2.32,2.46,1.87,1.88,2.41,1.97},
		    {2.35,2.00,1.95,0.00,2.05,1.78,2.08,2.27,2.14,2.14,2.38,2.17},
		    {2.06,2.23,2.21,2.05,0.00,2.35,2.23,2.18,2.30,1.98,1.74,2.06},
		    {2.12,2.04,2.23,1.78,2.35,0.00,2.21,2.12,2.21,2.12,2.17,2.23},
		    {2.27,2.38,2.32,2.08,2.23,2.21,0.00,2.04,2.44,2.19,1.74,2.13},
		    {2.34,2.36,2.46,2.27,2.18,2.12,2.04,0.00,2.19,2.09,1.71,2.17},
		    {2.57,2.23,1.87,2.14,2.30,2.21,2.44,2.19,0.00,1.81,2.53,1.98},
		    {2.43,2.36,1.88,2.14,1.98,2.12,2.19,2.09,1.81,0.00,2.00,1.52},
		    {1.90,2.57,2.41,2.38,1.74,2.17,1.74,1.71,2.53,2.00,0.00,2.33},
		    {2.41,2.34,1.97,2.17,2.06,2.23,2.13,2.17,1.98,1.52,2.33,0.00}
	        };
		int n=input[0].length;    // number of data objects
		double[][] output=MDSJ.classicalScaling(input); // apply MDS
		for(int i=0; i<n; i++) {  // output all coordinates
		    System.out.println(output[0][i]+" "+output[1][i]);
		}
	}
}
```
In the source code example MDSJExample.java a 12 x 12 matrix of dissimilarities is set up; see below for an explanation of this sample data set. Classical scaling is used to generate a two-dimensional configuration of the 12 objects.

Usage from the command line: MDSJ can be used as a standalone application from the command line
```
    starting the JAR file: java -jar mdsj.jar or
    through addressing its main class: java -classpath mdsj.jar mdsj.MDSJ
```
The following is the standard help output by MDSJ when called without parameters. In the syntax below, the command MDSJ is to be replaced by the command correspondig to your settings, e.g., java -jar mdsj.jar.

Calling MDSJ from the command line
```
software/mdsj> java -jar mdsj.jar                                         
MDSJ - Multidimensional Scaling for Java v0.2  (c) 2009 University of Konstanz  
  usage: MDSJ  [options]  infile  [outfile]        see manual for more details
  options
   -dD   output dimensions (default: D=2)
   -eE   use exponential weight=dissimilarity^E (default: E=0)
   -fF   data format: -fm matrix (default), -fl list, -fo optimized list
   -q    quiet mode, do not print analysis results
   -rR   stress minimization for at most R rounds
   -sS   stress minimization until relative change is below 10^(-S)
   -tT   stress minimization for up to T milliseconds
  example:  MDSJ  -t2000  -s4 -d3  -q  in.txt  out.txt
  -rR -sS -tT may be used jointly (termination once any condition holds)
  output is written to stdout when no outfile specified
```
software/mdsj> _

It reads an input text file infile containing the input dissimilarities and writes an output text file outfile containing the coordinates computed by MDS. Each line in the input file represents one row in the input matrix. The entries must be parseable as doubles and separated by at least one blank. See nations.txt for a sample file. When an output file for the final coordinates is specified, it is in the same format, i.e., each line contains the coordinates for one object in each dimension. If no outfile is specified, the coordinates are written to the standard output.

A sample data file: Wish (1971) asked 18 students about their perception of similarity (1=very dissimilar, 9=very similar) between 12 nations: Brazil, Congo, Cuba, Egypt, France, India, Israel, Japan, China, UdSSR, USA, Yugoslavia. Every similarity score is converted to a dissimilarity by dissimilarity = sqrt(9-similarity) and can be used as MDS input.

Classical Scaling turns these dissimilarities (nations.txt) into coordinates (nations-cmds.txt), which can be processed further, e.g., plotted with gnuplot.

The data is due to: Wish, Individual differences in perceptions and preferences among nations, in: King and Tigert (eds.), Attitude research reaches new heights. Am. Marketing Assoc., 1971. Original data set of similarity scores.
Version History

    v0.2 [2009-11-18]: Added features. Made linear algebra computations a bit more robust. Extended command line interface.
        Detailed spectral analysis of input dissimilarity matrix
        Stress Minimization with arbitrary weight matrix
        Verbose/quiet mode
        IO via standard input/output
        Sparse Stress Minimization
        Customizable termination criterion
    v0.1 [2008-06-11]: First pre-alpha release.

Some features are candiates for inclusion in future versions:

    Nonmetric Scaling
    Order Constraints
    Procrustes Analysis
    Unfolding

Conditions of Use

License Conditions: MDSJ is available under the terms and conditions of the Creative Commons License "by-nc-sa" 3.0. This means that you can

    freely copy, share, and distribute the library at no cost and
    re-use the library as a component in your software,

as long as you

    include the citation below (by),
    do not use MDSJ for any commercial purposes (nc), and
    apply these conditions to all your pieces of software that make use of MDSJ (sa). 

Please feel free to contact us for any questions regarding these conditions.

Citation: "Algorithmics Group. MDSJ: Java Library for Multidimensional Scaling (Version 0.2). Available at http://www.inf.uni-konstanz.de/algo/software/mdsj/. University of Konstanz, 2009."

Disclaimer: The MDSJ Java library ("software") is developed and maintained in the Algorithmics Group, Department of Computer & Information Science, University of Konstanz, Germany ("author"). Some rights reserved. The software is provided "AS IS", with no warranty, express or implied, including but not limited to the implied warranties of merchantability and fitness for a particular use. In no event shall the author be liable for any damages, direct or indirect, even if advised of the possibility of such damages. If you do not accept these restrictions, you do not have permission to download or use MDSJ.
Contact

Please let us know what you use MDSJ for. Comments, suggestions, ideas, and bug reports are welcome and will help us in improving the quality of the software.

Corresponding author: Christian Pich. (no current contact info known)
