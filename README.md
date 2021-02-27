# RKF
Implementation of Runge-Kutta Fehlberg method to numerically solve system of ODEs.

```
import numpy as np
import matplotlib.pyplot as plt 
import time
from RKF import rkf
import matplotlib.animation as animation

def lorenz(t,u):
    s=10
    r=24
    b=8/3
    x,y,z=u
    vx=s*y-s*x
    vy=r*x-x*z-y
    vz=x*y-b*z
    return np.array([vx,vy,vz])

x0=[2,2,2]

t,u  = rkf( f=lorenz, a=0, b=1e+1, x0=x0, atol=1e-8, rtol=1e-6 , hmax=1e-1, hmin=1e-40,plot_stepsize=True).solve()

x,y,z= u.T

plt.style.use('dark_background')
fig = plt.figure()
ax = fig.gca(projection='3d')
ax.set_axis_off()
ax.plot(x,y,z,lw=0.5,c='whitesmoke')
# plt.show()

def rotate(angle):
    ax.view_init(elev=7.,azim=angle)

print("Making animation")
rot_animation = animation.FuncAnimation(fig, rotate, frames=np.arange(0, 600, 2), interval=36)
rot_animation.save('lorenz.gif', dpi=400, writer='imagemagick')

```
[![lorenz.gif](https://i.postimg.cc/C1QtR7xv/lorenz.gif)](https://postimg.cc/Fd0Gqjcc)
