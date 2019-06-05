# Lorenz-Curve
# Hello, this data science project is showing a contribution to the common population of the bottom countries. The program produces a PNG file with the results. 

import numpy as np
from matplotlib import pyplot as plt

def LorenzCurve():
    curve = np.load('pop2010.npy')

    def f(x):
        plot_ = np.linspace(1,100)
        y = []
       #x = []
        for val in plot_:
            plotVals = curve[curve <= np.percentile(curve, val)] #looked up function on google
            sums = (np.sum(plotVals) / (float(np.sum(curve))))
            plot_line = (sums * 100.0)
            y.append(plot_line)
        
        graph = (np.trapz(plot_, plot_)) - (np.trapz(y, plot_))
        
        values = graph / float(np.trapz(plot_, plot_))
        
        return(plot_, y, values)
 

    plot_, outcome, values = f(curve)
   #f(curve) = plot_, outcome, values
    plt.figure()
    plt.title("Lorenz Curve")
    plt.ylabel("Wealth")
    plt.xlabel("Population")
    
    
    plt.plot(plot_, outcome, label="Actual contribution")
    plt.plot(plot_, plot_, '--', label="'The would be' contribution.")
    plt.legend()
    
    plt.savefig('population-lorenz.png', dpi = 200)
    plt.show()

LorenzCurve()
