#边缘检测算法实现 in java

1.Robert Gradient

![Robert](https://github.com/vienan/Edge-Detection-Algorithm/blob/master/Robert%20Gradient.png)

####Code

```java
 public Bitmap RobertGradient(Bitmap myBitmap){  
        // Create new array  
        int width = myBitmap.getWidth();  
        int height = myBitmap.getHeight();  
        int[] pix = new int[width * height];  
        myBitmap.getPixels(pix, 0, width, 0, 0, width, height);  
        Matrix dataR=getDataR(pix, width, height);  
        Matrix dataG=getDataG(pix, width, height);  
        Matrix dataB=getDataB(pix, width, height);  
        //Matrix dataGray=getDataGray(pix, width, height);  
        /////////////////////////////////////////////////////////  
        dataR=eachRobertGradient(dataR,width,height);  
        dataG=eachRobertGradient(dataG,width,height);  
        dataB=eachRobertGradient(dataB,width,height);  
        ///////////////////////////////////////////////////////////////  
        // Change bitmap to use new array  
        Bitmap bitmap=makeToBitmap(dataR, dataG, dataB, width, height);   
        myBitmap = null;  
        pix = null;  
        return bitmap;  
    }  
    private Matrix eachRobertGradient(Matrix tempM,int width,int height){  
        int i,j;  
        for(i=0;i<width-1;i++){  
            for(j=0;j<height-1;j++){  
                int temp=Math.abs((int)tempM.get(i, j)-(int)tempM.get(i,j+1))  
                         +Math.abs((int)tempM.get(i+1,j)-(int)tempM.get(i,j+1));  
                tempM.set(i, j, temp);  
            }  
        }  
        return tempM;  
    }  

```

2.Sobel Gradient

![Sobel](https://github.com/vienan/Edge-Detection-Algorithm/blob/master/%20Sobel%20Gradient.png)

####Code
```java
public Bitmap SobelGradient(Bitmap myBitmap){  
        // Create new array  
        int width = myBitmap.getWidth();  
        int height = myBitmap.getHeight();  
        int[] pix = new int[width * height];  
        myBitmap.getPixels(pix, 0, width, 0, 0, width, height);  
        Matrix dataR=getDataR(pix, width, height);  
        Matrix dataG=getDataG(pix, width, height);  
        Matrix dataB=getDataB(pix, width, height);  
        Matrix dataGray=getDataGray(pix, width, height);  
        /////////////////////////////////////////////////////////  
        dataGray=eachSobelGradient(dataGray, width, height);  
        dataR=dataGray.copy();  
        dataG=dataGray.copy();  
        dataB=dataGray.copy();  
        ///////////////////////////////////////////////////////////////  
        // Change bitmap to use new array  
        Bitmap bitmap=makeToBitmap(dataR, dataG, dataB, width, height);   
        myBitmap = null;  
        pix = null;  
        return bitmap;  
    }  
    private Matrix eachSobelGradient(Matrix tempM,int width,int height){  
        int i,j;  
        Matrix resultMatrix=tempM.copy();  
        for(i=1;i<width-1;i++){  
            for(j=1;j<height-1;j++){  
                int temp1=Math.abs(((int)tempM.get(i+1, j-1)+2*(int)tempM.get(i+1, j)+(int)tempM.get(i+1,j+1))  
                         -(((int)tempM.get(i-1,j-1)+2*(int)tempM.get(i-1,j)+(int)tempM.get(i-1,j-1))));  
                int temp2=Math.abs(((int)tempM.get(i-1, j+1)+2*(int)tempM.get(i, j+1)+(int)tempM.get(i+1,j+1))  
                         -(((int)tempM.get(i-1,j-1)+2*(int)tempM.get(i,j-1)+(int)tempM.get(i+1,j-1))));  
                int temp=temp1+temp2;  
                resultMatrix.set(i, j, temp);  
            }  
        }  
        return resultMatrix;  
    }  
```

3.Laplace Gradient

![Laplace](https://github.com/vienan/Edge-Detection-Algorithm/blob/master/Laplace%20Gradient.png)

####Code
```java
public Bitmap LaplaceGradient(Bitmap myBitmap){  
        // Create new array  
        int width = myBitmap.getWidth();  
        int height = myBitmap.getHeight();  
        int[] pix = new int[width * height];  
        myBitmap.getPixels(pix, 0, width, 0, 0, width, height);  
        Matrix dataR=getDataR(pix, width, height);  
        Matrix dataG=getDataG(pix, width, height);  
        Matrix dataB=getDataB(pix, width, height);  
        Matrix dataGray=getDataGray(pix, width, height);  
        /////////////////////////////////////////////////////////  
        dataGray=eachLaplaceGradient(dataGray,width,height);  
        dataR=dataGray.copy();  
        dataG=dataGray.copy();  
        dataB=dataGray.copy();  
        ///////////////////////////////////////////////////////////////  
        // Change bitmap to use new array  
        Bitmap bitmap=makeToBitmap(dataR, dataG, dataB, width, height);   
        myBitmap = null;  
        pix = null;  
        return bitmap;  
    }  
    private Matrix eachLaplaceGradient(Matrix tempM,int width,int height){  
        int i,j;  
        Matrix resultMatrix=tempM.copy();  
        for(i=1;i<width-1;i++){  
            for(j=1;j<height-1;j++){  
                int temp=Math.abs(5*(int)tempM.get(i, j)-(int)tempM.get(i+1,j)  
                        -(int)tempM.get(i-1,j)-(int)tempM.get(i,j+1)-(int)tempM.get(i,j-1));  
                resultMatrix.set(i, j, temp);  
            }  
        }  
        return resultMatrix;  
    }  
```
