# Main-Project-Code

Code for Main Project 
function imageData = whitebalance(imageData) 

% WHITEBALANCE forces the average image color to be gray.

% Find the average values for each channel. 

avg_rgb = mean(mean(imageData)); 

% Find the average gray value and compute the scaling 

% factor. 

factors = max(mean(avg_rgb), 150)./avg_rgb; 

% Adjust the image to the new gray value. 

%  imageData(:,:,1) =uint8(imageData(:,:,1)*factors(1)); 

%  imageData(:,:,2) = uint8(imageData(:,:,2)*factors(2)); 

%  imageData(:,:,3) = uint8(imageData(:,:,3)*factors(3)); 

 imageData(:,:,1) =histeq(imageData(:,:,1));

  imageData(:,:,2) = histeq(imageData(:,:,2));

  imageData(:,:,3) =histeq(imageData(:,:,3)) ; 

%imageData =uint8(imageData*factors);
Main code 
clear all;

close  all;

clc;

x=imread('und5.png');

%x=imresize(x,[223 298]);

figure

imshow(x)

xr=x(:,:,1);

xg=x(:,:,2);

xb=x(:,:,3);

[m n]=size(xr);

xr_m=[];

alp=1.1

for i=1:m

    for j=1:n

        z1(i,j)=(alp*xg(i,j)+(1-alp)*xb(i,j))-xr(i,j);

        z2(i,j)=(alp*xg(i,j)+(1-alp)*xb(i,j))/(xr(i,j)+xg(i,j)+xb(i,j));

        xr_m(i,j)=xr(i,j)+z1(i,j)*z2(i,j);

     

        

        

    end 

end

     

figure

subplot(211)

imshow(xr)

subplot(212)

imshow(uint8(xr_m))

x1=[];

x1(:,:,1)=xr_m;

x1(:,:,2)=x(:,:,2);

x1(:,:,3)=x(:,:,3);

x2=[];

x2(:,:,1)=x1(:,:,1)/max(max(x1(:,:,1)));

x2(:,:,2)=x1(:,:,2)/max(max(x1(:,:,2)));

x2(:,:,3)=x1(:,:,3)/max(max(x1(:,:,3)));

figure

imshow(uint8(x1) )

s2=whitebalance(uint8(x1));

figure

imshow(uint8(s2))

r=entropy(uint8(s2));

s3(:,:,1)=histeq(s2(:,:,1));

s3(:,:,2)=histeq(s2(:,:,2));

s3(:,:,3)=histeq(s2(:,:,3));
