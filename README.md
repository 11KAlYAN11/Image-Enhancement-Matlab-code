# Image-Enhancement-Matlab-code

% Read input image
img = imread('temple.jpeg');

% Define gamma correction parameters
gamma = 0.8; % Gamma value for contrast improvement
alpha = 1.5; % Alpha value for brightness adaptation

% Compute average logarithmic value
avg = exp(mean(log(double(img(:)))));

% Perform brightness adaptation
img_adapted = alpha * img + (1 - alpha) * avg;

% Perform gamma correction for contrast improvement
img_gamma_corrected = 255 * (double(img_adapted) / 255).^gamma;

% Perform color level remapping
min_val = min(img_gamma_corrected(:)); % Minimum input value
max_val = max(img_gamma_corrected(:)); % Maximum input value
new_min = 20; % New minimum output value
new_max = 250; % New maximum output value
img_color_corrected = (double(img_gamma_corrected) - min_val) / (max_val - min_val) * (new_max - new_min) + new_min;

% Convert the image back to uint8 format
img_color_corrected = uint8(img_color_corrected);

% Display enhanced image
figure;
imshow(img),title('Original Image');
figure;
imshow(uint8(img_adapted)),title('brightness adaption image');
figure;
imshow(uint8(img_gamma_corrected)),title('contrast improment image');
figure;
imshow(uint8(img_color_corrected)),title('color correction image');

