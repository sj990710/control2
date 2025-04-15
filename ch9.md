![image](https://github.com/user-attachments/assets/7496c27d-22bf-4b15-8e34-008a4ddc42dd)
# matlab
```
s = tf('s'); 
L = (3 * (1 + 5 * s)) / (s * (s + 4) * (1 + 2 * s + 2 * s^2))

bode(L);
grid on;
```
![image](https://github.com/user-attachments/assets/a3dd4358-5a57-4571-8e33-654b52442a7b)
# 수기
![image](https://github.com/user-attachments/assets/e84985fd-2aa8-4bd0-9c56-95d125c77e46)
***

![image](https://github.com/user-attachments/assets/644a3fa5-ee8d-400f-b207-b473d731dc28)
# matlab
```
K = 4;
s = tf('s');
L = K * (1 + s/20) / (s * (1 + s/8) * (1 + s + 10));

figure;
bode(L);
grid on;

[mag, phase, w] = bode(L);

w_c_index = find(mag >= 1, 1);
omega_c = w(w_c_index);

phase_at_wc = phase(w_c_index);
phase_margin = 180 + phase_at_wc;

disp(['교차 주파수 (w_c): ', num2str(omega_c), ' rad/s']);
disp(['위상 여유 (P.M.): ', num2str(phase_margin), ' degrees']);

```
![image](https://github.com/user-attachments/assets/5ff6c46b-a579-43a2-a755-442b9e0786b1)
![image](https://github.com/user-attachments/assets/5d0ee09c-ea95-4e03-8aee-a7a8f296d744)

# 수기
![image](https://github.com/user-attachments/assets/749acc36-9176-4a77-82f4-1cc71644d2ba)
***
![image](https://github.com/user-attachments/assets/1dec882f-1138-407f-97a1-629ee2779d25)
# matlab
```
K_positive = 4;  % 양수 K 값
K_negative = -4;  % 음수 K 값

s = tf('s');  % Laplace 변수 s 정의

L_positive = K_positive / (s - 5);  % 양수 K에 대한 전달 함수
L_negative = K_negative / (s - 5);  % 음수 K에 대한 전달 함수

figure;

% Nyquist 선도 그리기 (양수 K)
subplot(1, 2, 1);
nyquist(L_positive);
title('Nyquist Plot for K > 0');
grid on;
hold on;
plot(-1, 0, 'ro', 'MarkerFaceColor', 'r');
text(-1.1, 0, '-1 + 0j', 'Color', 'r');

% Nyquist 선도 그리기 (음수 K)
subplot(1, 2, 2);
nyquist(L_negative);
title('Nyquist Plot for K < 0');
grid on;
hold on;
plot(-1, 0, 'ro', 'MarkerFaceColor', 'r');
text(-1.1, 0, '-1 + 0j', 'Color', 'r');
```
![image](https://github.com/user-attachments/assets/8d28417d-aef3-43d9-93dd-ba5a48e5ce8e)

# 수기
![image](https://github.com/user-attachments/assets/b495f2d2-9fbd-4a33-855d-522af5cdabb1)
***
![image](https://github.com/user-attachments/assets/6f1c5e71-914d-4b7f-912b-4753f67e4bf8)
## (a) : 안정
# matlab
```
K_min = 0;
K_max = 10;
step = 0.1;
stable_K = [];
s = tf('s');
L = @(K) K / (s * (s^2 + 2*s + 5));

for K_test = K_min:step:K_max
    L_test = L(K_test);
    [Gm, Pm, Wcg, Wcp] = margin(L_test);
    if Gm > 1
        stable_K = [stable_K, K_test];
    end
end

disp(['안정한 K 범위: ', num2str(min(stable_K)), ' <= K <= ', num2str(max(stable_K))]);

K = 1;
L_plot = L(K);

figure;
nyquist(L_plot);
grid on;
title('Nyquist Plot for L(s) = K / (s * (s^2 + 2s + 5))');
hold on;

plot(-1, 0, 'ro', 'MarkerFaceColor', 'r');
text(-1.1, 0, '-1 + 0j', 'Color', 'r');

xlim([-5, 5]);
ylim([-5, 5]);

set(gca, 'FontSize', 12);
```
![image](https://github.com/user-attachments/assets/5210862d-c547-4f94-a8ce-394fabb92d8c)

![image](https://github.com/user-attachments/assets/c18e26a1-cd21-412e-98ff-863ea877f30b)
# 수기
![image](https://github.com/user-attachments/assets/139f00d4-879d-474f-bee5-0886430512f5)

## (b) : 불안정
# matlab
```
K = 1;
s = tf('s');
L = K * (s + 2) / (s^2 * (s^2 + 5));

figure;
nyquist(L);
grid on;
title('Nyquist Plot for L(s) = K * (s + 2) / (s^2 * (s^2 + 5))');
hold on;

plot(-1, 0, 'ro', 'MarkerFaceColor', 'r');
text(-1.1, 0, '-1 + 0j', 'Color', 'r');

```
![image](https://github.com/user-attachments/assets/dc916711-b104-4477-873f-ad961e53b362)

# 수기
![image](https://github.com/user-attachments/assets/b904fd76-90bb-4fed-be91-af71886d1406)
