Welcome to the FiberByPy package!

This code package was written by Edward B. Trigg.
Copyright 2017.


#####  What does this code do?  #####

This code performs 2D fits of fiber scattering (i.e., X-ray scattering of materials with cylindrical symmetry).

The code assumes vertical mirror symmetry and inversion symmetry of the scattering pattern, making it useful for 
cases where the cylindrical axis is perpendicular to the incident X-ray beam. 

This code not only contains the math to describe peak shapes in 3D reciprocal space and map them onto the detector,
but it also contains several powerful fitting algorithms to ensure an optimized fit. The code features a user-
friendly command-line interface.


#####  What do I need to run this code?  #####

You will need Python version 2.7 and the corresponding Numpy, Scipy, and MatPlotLib packages. These are available 
for free at python.org and sourceforge.net. 


#####  How can I understand the math used in this code for fitting?  #####

See the following article:
 Burger, Hsiao, Chu. "Preferred Orientation in Polymer Fiber Scattering." Polymer Reviews, 2010, 50(1), 91-111.
 

#####  What format should my data be in?  #####

You should have a series of I vs. q traces. Each trace corresponds to a constant azimuthal angle. Each trace is
in its own file. I recommend using two-degree azimuthal wedges of your detector. For example, one file would contain
I vs. q averaged over all azimuthal angles that are between 0 and 2 degrees. The next would contain the same for 
2 to 4 degrees. See the example file for details. Note that all "wedge" files should have exactly the same q values.

I recommend taking a look at the example data provided, to make sure your data is in the right format.


#####  How do I get started?  #####

Just run the file called "main.py" and start typing commands. You can also create a text file with a series of 
commands, and call the text file from the command line to run all of the commands in the file.

I recommend taking a look at the "example_cmds.txt" file to get a sense of how to use the commands. 

To start playing with the example data, after running "main.py", just type "readcmds example_cmds.txt" in the 
command line and hit enter. This will load in the example data and recreate a fit result. This is plotted in
the file "tmp.png". You can change the fitting parameters and then replot using the "plot" command, and this 
will update "tmp.png".


#####  What commands can I use?  #####

open <filebasepath> <range(__)> <range(__)>     -- opens experimental data (see example)
plot                              -- plots data, or plots data + current fit (wopen opens fig in windows photo viewer)
plotdiff                          -- plots exp/fit figure, and difference figure
saveplot filename data/fit <wopen>     -- plots data and saves with specified filename
func <action> <arg>  -- adds/removes a fit function or fix/unfix
                                          <action>=add, rm
										<arg>=func type for add, or func number for rm
change <fitfunc_n> <parameter_n> <newvalue>  -- manually change a fitting parameter value
changeall <fitfunc_n> <newvalue> <newvalue> ...  -- change all parameters in a function at once
changestep <fitfunc_n> <parameter> <newstep> -- manually change parameter step size
vrange <vmin> <vmax>              -- change color range
setcalclimit <fitfunc_n> <x> <value> -- set limit of calculation of fitfunc_n if type = peaktype1. x = qmin, qmax, or phimin.
setexprange <qmin> <qmax>         -- set range of experimental (and fit) data (impacts plot range)
printbounds                       -- print ranges of all parameters in all functions
fit <type> <func_n> <no_iter>     -- run the fit (type = stepper or deriv)
fitm <type> <func_n list> <no_iter> -- fits each func_n in func_n list (comma-sepatated, no spaces)(type = stepper or deriv)
fita <type> <func_n:func_n:...> <no_iter> -- alternates between all func_n functions (<no_iter> iterations per function) 
fitlim <qlo> <qhi> <philo> <phihi> -- set fitting range (x axis only)
plot_fitlim                       -- toggle whether to trace fit limits on plot
printssd                          -- print ssd for current fit
fix <fitfunc_n> <parameter>       -- toggle whether to fix a fitting parameter or allow fit
q                                 -- quit program
savestate <filename>              -- save current state to file
loadstate <filename> <nofile>       -- open saved state, include "nofile" if not open exp
readcmds <cmd_filename>           -- reads a series of commands from a file (one cmd per line)
