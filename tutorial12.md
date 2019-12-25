	TASK1: Using the code snippets provided, create your own Object Tracking script using regionprops. 
```
clc;clear;close all;
clc;clear;close all;
video = VideoReader('Video_ObjectTracking.avi');
currentFrame = readFrame(video);

while hasFrame(video)
    frame = readFrame(video); %Read current frame in the loop
	previousFrame = currentFrame; %We store previous frame as the old frame
	currentFrame = frame; %We assign the current frame to its variable
	difference = imabsdiff(currentFrame, previousFrame); %Absolute difference
	thresh = 0.85*mean(difference(difference>0));
    isdifferent = difference > thresh; %Image threshold
    
    myStrel = strel('disk',10); 
    erosion = imerode(isdifferent, myStrel);
    myStrel2 = strel('disk', 50); %modify this value to make regions more bigger
    dilation = imdilate(erosion, myStrel2);
    myBwMask= imfill(dilation, 'holes');   

    MyRegionProps = regionprops(myBwMask , 'Centroid', 'BoundingBox', 'Area');

    imshow(frame);
    hold on;

    for k = 1:numel(MyRegionProps)
        if MyRegionProps(k).Area>1000
            plot(MyRegionProps(k).Centroid(1), MyRegionProps(k).Centroid(2), 'r*');
            rectangle('Position',MyRegionProps(k).BoundingBox([1:2,4:5]),'EdgeColor','r','LineWidth', 2,'LineStyle', '-');
        end
    end
    hold off;
end
```
![task](src/weak12/1-1.png 'xxx')


	 TASK2: Download ‘Puppet.avi’ and test the code. Find the most suitable morphology values to obtain the cleanest result. 
```
 code seems like task1
```


	TASK3: See how these values look with the ‘Cars.mp4’ video from last week
```
 code seems like task1
```
![task](src/weak12/2.png 'xxx')


	TASK4: Explore the use of regionprops and show regions above 1000px only using the area property
```
clc;clear;close all;
video = VideoReader('Video_ObjectTracking.avi');
currentFrame = readFrame(video);

while hasFrame(video)
    frame = readFrame(video); %Read current frame in the loop
	previousFrame = currentFrame; %We store previous frame as the old frame
	currentFrame = frame; %We assign the current frame to its variable
	difference = imabsdiff(currentFrame, previousFrame); %Absolute difference
	thresh = 0.85*mean(difference(difference>0));
    isdifferent = difference > thresh; %Image threshold
    
    myStrel = strel('disk',10); 
    erosion = imerode(isdifferent, myStrel);
    myStrel2 = strel('disk', 300); %modify this value to make regions more bigger
    dilation = imdilate(erosion, myStrel2);
    myBwMask= imfill(dilation, 'holes');   

    MyRegionProps = regionprops(myBwMask , 'Centroid', 'BoundingBox', 'Area');

    imshow(frame);
    hold on;

    for k = 1:numel(MyRegionProps)
        if MyRegionProps(k).Area>1000
            plot(MyRegionProps(k).Centroid(1), MyRegionProps(k).Centroid(2), 'r*');
            rectangle('Position',MyRegionProps(k).BoundingBox([1:2,4:5]),'EdgeColor','r','LineWidth', 2,'LineStyle', '-');
        end
    end
    hold off;
end


```
![task](src/weak12/4-1.png 'xxx')