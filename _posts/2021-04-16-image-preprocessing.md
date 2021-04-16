---
layout: post
title:  "Data Preprocessing"
author: Eujin
categories: [  ]
image: 
tags: []
published: no
---

이미지 전처리 기술에는 크게 4 가지 유형이 있습니다.

Pixel brightness transformations/ Brightness corrections
Geometric Transformations
Image Filtering and Segmentation 
Fourier transform and Image restoration
Pixel brightness transformations/brightness corrections (픽셀 밝기 변환)

Contrast 향상은 인간과 컴퓨터 비전, 이미지 처리에서 중요한 영역입니다. 의료 이미지 처리에 널리 사용되며 음성 인식, 텍스처 합성 및 기타 여러 이미지 / 비디오 처리 애플리케이션의 전처리 단계로 사용됩니다. 가장 일반적인 픽셀 밝기 변환 작업은 다음과 같습니다.

1.  Gamma Correction (감마 보정)
감마 보정은 소스 이미지 픽셀에 대해 비선형 작업을 수행하며 이미지의 채도를 변경합니다. Power law transform 이라고도 부릅니다.
먼저 이미지 픽셀 강도를 [0, 255]에서 [0, 1.0]까지 범위로 조정해야 합니다. 다음 방정식을 적용하여 output gamma corrected 이미지를 얻습니다. I는 입력 이미지이고 G는 감마 값입니다.
O = I ^ (1 / G)
출력 이미지 O는 [0, 255] 범위로 다시 조정됩니다.
감마 값이<1 이면 이미지가 스펙트럼의 더 어두운 쪽으로 이동하고 감마 값이>1이면 이미지가 더 밝아집니다. 감마 값 G = 1은 입력 이미지에 영향을 주지 않습니다.
2. Sigmoid Stretching
Sigmoidal stretch는 극단에서 충분한 contrast를 유지하면서 이미지의 moderate 픽셀 값을 강조하도록 되어있습니다.
Sigmoid Function (S 자 모양의 곡선)를 따라 모든 픽셀 값을 배치합니다. 그 결과로 매우 밝은 영역과 매우 어두운 영역에서는 대비가 적고 이러한 영역 사이의 영역에서 더 많은 대비가 발생합니다.
Sigmoid stretching은 거의 모든 이미지에 이상적이며 이미지에 구름과 물이 있을 때 더욱 좋습니다.
3. Histogram equalization
Histogram equalization은 히스토그램의 intensity 분포를 변경하여 이미지의 contrast를 조정하기 위해 이미지를 처리하는 방법입니다. 목적은 이미지와 관련된 누적 확률 함수에 선형 추세를 제공하는 것입니다.
히스토그램 equalization은 종종 사진을 비현실적으로 만듭니다. 하지만 전경이 모두 밝거나 어두운 이미지에 유용합니다. 특히 열 화상, 위성 또는 X-ray 이미지와 같은 과학적 이미지에는 매우 유용합니다.
https://www.researchgate.net/publication/283727396_Image_enhancement_by_Histogram_equalization

Geometric Transformations

이미지의 픽셀 위치가 수정됩니다. 기하학적 변환에는 두 가지 기본 단계가 있습니다. 이미지에서 픽셀의 물리적 재배열의 공간적 변환과 Grey level interpolation(변환 된 이미지에 그레이 레벨을 할당)입니다.

4. Scaling
이미지 resizing (x’=x*Sx / y’=y*Sy)
5. Translation
Shifting of object location (x’=x+x / y’=y+y)
6. Rotation
회전 (x’=xcos- ysin/ y’=xsin+ycost)
7. Shearing
Shifting pixels horizontally (x’=x+yBx / y’=xBy+y)
8. Affine Transformation
Scaling, Translation, Rotation, Shearing을 모두 적용시킨 것입니다. Merge the above transformations into one matrix.
(x’=a1*x+a2*y+a3 / y’=b1*y+b2*y+b3)
Affine Transformation은 선의 parallelism을 유지하면서 이미지의 기하학적 구조를 수정하는 데 도움이됩니다.
위성 이미지와 같은 비이상적인 카메라 각도에서 발생하는 기하학적 왜곡 및 변형을 수정하는데도 사용됩니다.

9. Nearest Neighbor Interpolation
Interpolation->이미지 f의 샘플 F가 주어지면 interpolation은 샘플 포인트가 아닌 (x, y)에 대해서도 f (x, y) 값을 계산하도록 하는 것입니다.
목표는 샘플링 된 함수F 만 주어진 경우 임의의 x에 대한 f (x)의 추정치를 찾는 것입니다.
https://arxiv.org/pdf/1211.1768.pdf
Image Interpolation은 작은 이미지를 구성하는 픽셀 수를 늘려 작은 이미지를 크게 만드는 프로세스입니다.
위성 이미지, 생의학 이미지, 군사 및 소비자 가전 분야에서 필요한 이미지 프리 프로세싱 방식입니다. 이것은 가장 빠른 Interpolation 방법이지만 결과 이미지에 들쭉날쭉 한 가장자리가 포함될 수 있습니다.

10. Linear Interpolation
가장 가까운 두 픽셀을 조사하여 그 사이에 선을 그리고 해당 선을 따라 하나의 픽셀 값을 output으로 지정합니다.
11. Bilinear Interpolation
가장 가까운 4 개의 픽셀을 조사하고 조사 된 픽셀의 근접성과 밝기를 기반으로 가중치 평균을 생성하고 해당 값을 출력 이미지의 픽셀에 할당합니다.
더 높은 정확도가 필요한 경우 cubic convolution interpolation을 사용하는게 좋습니다. 그러나 정지된 이미지의 경우 bilinear 및 cubic convolution 방법의 차이는 일반적으로 크게 나지 않습니다.
12. Cubic Convolution Interpolation
1D에서는 8픽셀, 2D에서는 16 픽셀을 조사합니다. 이 방법을 사용하면 오류가 최소화되므로 출력 이미지에서 미세한 디테일을 최대한 보존 할 수 있습니다. 그러나 더 많은 처리 시간이 필요합니다.
Image Filtering 

필터를 사용하는 목적은 이미지 속성을 수정 또는 향상시키거나 가장자리, 모서리 및 blob와 같이 그림에서 중요한 정보를 추출하는 것입니다.

13. Low Pass Filtering(Smoothing): average nearby pixels
Low pass filter은 대부분의 smoothing method의 기초입니다. 주변 픽셀을 평균화하여 픽셀 값 간의 차이를 줄여 이미지를 매끄럽게 만듭니다.
Low pass filter를 사용하면 high frequency info를 줄이면서 이미지 내 low frequency info를 유지하는 경향이 있습니다.
14. High Pass Filtering(Edge Detection, Sharpening): emphasize details in image

High pass filter은 대부분의 샤프닝 방법의 기초입니다. High pass filter은 low frequency info를 줄이면서 이미지 내에서 high frequency info를 유지하는 경향이 있습니다. Low pass filter의 반대 역할을 한다고 생각하면 됩니다.
15. Directional Filtering: Edge detector that can be used to compute the slopes of an image.

Directional filter은 이미지의 1st derivative를 계산하는 데 사용할 수있는 edge detector입니다. 1st derivative(기울기)는 인접한 픽셀 값간에 큰 변화가 발생할 때 가장 큽니다.
이미지의 경우 x 및 y 방향 필터는 일반적으로 해당 방향의 미분을 계산하는 데 사용됩니다.

16. Laplacian Filtering: Edge detector used to compute the measuring rate at which the first derivatives(slopes) change.

Laplacian filter는 이미지의 2nd derivative를 계산하는 데 사용되는 edge detector로, 1st derivative가 변경되는 속도를 측정합니다. 이것은 인접한 픽셀 값의 변화가 edge 또는 연속 진행에서 발생하는지 결정합니다.
Laplacian filter 커널은 보통 배열 중앙에 cross 모양으로 음수를 포함합니다. 모서리는 0 또는 양수 값입니다. 중심 값은 음수 또는 양수일 수 있습니다.
예시
17. Median Filter: effective in the presence of impulse noise like Salt and Pepper noise.

Median filter은 smoothing technique중 하나입니다. 기본 아이디어는 각 픽셀을 인접한 픽셀의 중앙값으로 대체하는 것입니다. 그렇게 함으로써 소음으로 인한 일부 스파이크, 특히 salt and pepper noise를 제거합니다.
18. Wiener Filter: effective in the presence of random noise like Gaussian noise.
흔들림 또는 초점이 맞지 않는 상태로 인한 이미지의 blur를 제거하는 가장 중요한 기술은 Wiener 필터입니다. 
Image Segmentation

디지털 이미지 처리 및 분석에서 일반적으로 사용되는 기술로 이미지의 픽셀 특성에 따라 이미지를 여러 부분 또는 영역으로 분할합니다.

색상 또는 모양의 유사성에 따라 픽셀 영역을 클러스터링
전경에서 배경을 분리

<Non-contextual thresholding>

19. Simple Thresholding


모든 픽셀에 대해 동일한 threshold value가 적용됩니다. 픽셀 값이 threshold value보다 작으면 0으로 설정되고, 그렇지 않으면 최대 값으로 설정됩니다.

20. Adaptive Thresholding


Adaptive thresholding 알고리즘은 주변의 작은 영역을 기반으로 픽셀의 threshold를 결정합니다.
동일한 이미지의 여러 영역에 대해 서로 다른 threshold를 얻어 다양한 조명을 사용하는 이미지에서도 괜찮은 결과가 나옵니다.

21. Color Thresholding


https://ieeexplore.ieee.org/document/4723398
Color Thresholding은 그레이 스케일 아날로그보다 훨씬 더 관심있는 객체에 초점을 맞출 수 있습니다. 

<Contextual segmentation>

Pixel Connectivity
Region Similarity
Region Growing
Split-and-merge segmentation


<Texture segmentation>

Fourier Transform
Fourier Transform
ETC+ 추가 그 외
Sobel
Prewitt
Roberts
Laplacian of Gaussian (LoG)
Canny edge detection
basic global thresholding (BGT) 
Otsu's global thresholding (OGT)
