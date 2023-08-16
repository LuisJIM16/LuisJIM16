import numpy as np
import matplotlib.pyplot as plt

lamb=20
f = [10,15,20]; Nd = np.size(f)
h = [5,10,15]; Nd = np.size(h)
lado = 3

M = np. empty( (lado, lado, Nd) ); M. fill(np. NaN)
for jd in range(Nd):
  M[0,0,jd] = ((f[jd])/2) + ((h[jd])/2)
  M[0,1,jd] = (2*lamb) - h[jd]
  M[0,2,jd] = (-lamb) - ((f[jd])/2) + ((h[jd])/2)
  M[1,0,jd] = (2*lamb) - f[jd]
  M[1,1,jd] = -lamb
  M[1,2,jd] = f[jd]
  M[2,0,jd] = (-lamb) + ((f[jd])/2) - ((h[jd])/2)
  M[2,1,jd] = h[jd]
  M[2,2,jd] = (2*lamb) - ((f[jd])/2) - ((h[jd])/2)
del jd

mycmap = plt.get_cmap( 'plasma', 60)
fsize = 16

plt.figure(figsize=(13,5))
for jd in range(Nd):
  plt.subplot(1,Nd,1+jd)
  plt.matshow(M[:,:,jd],fignum=0,cmap=mycmap,vmin=-60,vmax=60)
  plt.colorbar(extend='both')
  plt.title('variable libre f='+str(f[ jd])+' y h='+str(h[jd]), fontsize=fsize-10)
  ax = plt.gca( )
  for i in range(lado):
    for j in range(lado):
      c = M[j, i, jd]
      ax.text(i, j, str(c), va= 'center', ha= 'center')
    del i 
  del jd
plt.suptitle( 'algunos cuadrados semimágicos 3x3 con constante '+str(lamb), fontsize=fsize)
