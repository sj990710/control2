![image](https://github.com/user-attachments/assets/88acc012-70e3-4774-b798-c9b1320c0ec1)
```
omega = logspace(-1, 2, 500);

L_jw = 10 ./ (1i * omega + 1).^2;

magnitude = abs(L_jw);
phase = angle(L_jw);

figure;

subplot(2, 1, 1);
semilogx(omega, 20*log10(magnitude));
title('Magnitude Response');
xlabel('Frequency (ω)');
ylabel('Magnitude (dB)');
grid on;

subplot(2, 1, 2);
semilogx(omega, rad2deg(phase));
title('Phase Response');
xlabel('Frequency (ω)');
ylabel('Phase (degrees)');
grid on;
```
![image](https://github.com/user-attachments/assets/fc699c59-ea07-422c-96a5-f2b3a398f5f6)

```
% 주파수 값들 정의
omega_values = [0, 0.5, 1, 2, 4, Inf];

% 크기와 위상을 저장할 배열 준비
magnitude_values = zeros(size(omega_values));
phase_values = zeros(size(omega_values));

for i = 1:length(omega_values)
    omega = omega_values(i);
    
    % L(jω) 계산: L(jω) = 10 / (jω + 1)^2
    L_jw = 10 / (1i * omega + 1)^2;
    
    % 크기 계산 (절댓값)
    magnitude_values(i) = abs(L_jw);
    
    % 위상 계산 (라디안 -> 도로 변환)
    phase_values(i) = rad2deg(angle(L_jw));
end

% 결과 출력
disp('주파수 | 크기 (Magnitude) | 위상 (Phase)');
disp([omega_values' magnitude_values' phase_values']);

```
![image](https://github.com/user-attachments/assets/7ac416e6-9772-4fa3-bbd3-53c6c32061a3)

![image](https://github.com/user-attachments/assets/bd938552-55b6-4491-94b6-63e8bc848e5a)
![image](https://github.com/user-attachments/assets/e684ca11-5cf6-472d-8785-dd6bbb1e0413)
```
% 주파수 범위 정의
omega = logspace(0, 3, 500); % 주파수 범위 1~1000

% 전달함수 G(jω) 계산
G_jw = 5000 ./ ((1i * omega + 70) .* (1i * omega + 500));

% 크기와 위상 계산
magnitude = abs(G_jw);
phase = angle(G_jw);

% 크기 응답 (dB) 계산
magnitude_dB = 20 * log10(magnitude);

% 그래프 그리기
figure;

% 크기 응답 플롯
subplot(2, 1, 1);
semilogx(omega, magnitude_dB);
title('Magnitude Response of G(jω)');
xlabel('Frequency (ω)');
ylabel('Magnitude (dB)');
grid on;

% 위상 응답 플롯
subplot(2, 1, 2);
semilogx(omega, rad2deg(phase));
title('Phase Response of G(jω)');
xlabel('Frequency (ω)');
ylabel('Phase (degrees)');
grid on;

% 주어진 주파수에서 크기와 위상 값 확인
omega_values = [10, 200, 700]; % w = 10, 200, 700

% 크기 계산 (dB)
magnitude_values = 20 * log10(abs(5000 ./ ((1i * omega_values + 70) .* (1i * omega_values + 500))));

% 위상 계산 (degrees)
phase_values = rad2deg(angle(5000 ./ ((1i * omega_values + 70) .* (1i * omega_values + 500))));

% 결과 출력
disp('주파수 (ω) | 크기 (dB) | 위상 (Phase)');
disp([omega_values' magnitude_values' phase_values']);
```
![image](https://github.com/user-attachments/assets/ca1fcbac-ec7c-4525-b65b-37ac2e101493)
![image](https://github.com/user-attachments/assets/b78bf5b2-8c28-4d34-b199-055239ee07eb)

![image](https://github.com/user-attachments/assets/7ef4c0b8-4925-407d-8526-abce5e208a10)

(a)
```
% 전달함수 T(s)와 T1(s) 정의
s = tf('s');
T = 100*(s-1)/(s^2 + 25*s + 100);  % T(s)
T1 = 100*(s+1)/(s^2 + 25*s + 100); % T1(s)

% T(s)의 Bode 선도
figure;
[mag, phase, omega] = bode(T);
mag = squeeze(mag); % 크기 응답
phase = squeeze(phase); % 위상 응답

% Bode 선도 그리기
subplot(2, 1, 1);
semilogx(omega, 20*log10(mag)); % 크기 응답 (dB)
title('Bode Plot of T(s)');
xlabel('Frequency (rad/s)');
ylabel('Magnitude (dB)');
grid on;

% 절점주파수 표시 (크기 응답에서 중요한 주파수)
hold on;
% 극점과 영점의 영향에서 계산된 절점주파수 값들
omega_zeros_poles = [5, 20]; % 예: s = -5, s = -20
for i = 1:length(omega_zeros_poles)
    % 절점주파수에서 크기가 0 dB에 근접한 지점 표시
    plot(omega_zeros_poles(i), 0, 'ro'); % 빨간 원으로 표시
end
legend('Magnitude', 'Zero/Pole Frequency');

% T1(s)의 Bode 선도
figure;
[mag1, phase1, omega1] = bode(T1);
mag1 = squeeze(mag1); % 크기 응답
phase1 = squeeze(phase1); % 위상 응답

% Bode 선도 그리기
subplot(2, 1, 1);
semilogx(omega1, 20*log10(mag1)); % 크기 응답 (dB)
title('Bode Plot of T1(s)');
xlabel('Frequency (rad/s)');
ylabel('Magnitude (dB)');
grid on;

% 절점주파수 표시 (크기 응답에서 중요한 주파수)
hold on;
% 극점과 영점의 영향에서 계산된 절점주파수 값들
omega_zeros_poles_1 = [5, 20]; % 예: s = -5, s = -20
for i = 1:length(omega_zeros_poles_1)
    % 절점주파수에서 크기가 0 dB에 근접한 지점 표시
    plot(omega_zeros_poles_1(i), 0, 'ro'); % 빨간 원으로 표시
end
legend('Magnitude', 'Zero/Pole Frequency');

```
![image](https://github.com/user-attachments/assets/91131dbf-ee8c-452a-8496-50c871ec09ea)

(b)
```
% 전달함수 T(s)와 T1(s) 정의
s = tf('s');
T = 100*(s-1)/(s^2 + 25*s + 100);  % T(s)
T1 = 100*(s+1)/(s^2 + 25*s + 100); % T1(s)

% T(s)의 Bode 선도
figure;
[mag, phase, omega] = bode(T);
mag = squeeze(mag); % 크기 응답
phase = squeeze(phase); % 위상 응답

% Bode 선도 그리기
subplot(2, 1, 1);
semilogx(omega, 20*log10(mag)); % 크기 응답 (dB)
title('Bode Plot of T(s)');
xlabel('Frequency (rad/s)');
ylabel('Magnitude (dB)');
grid on;

% 고주파수 영역에서 기울기 추정
% 대략적으로 10^2 부근과 10^3 부근에서 기울기 추정
high_freq_range = omega(omega > 10^2 & omega < 10^3);
high_mag = mag(omega > 10^2 & omega < 10^3);
slope_high = (20 * log10(high_mag(end)) - 20 * log10(high_mag(1))) / (log10(high_freq_range(end)) - log10(high_freq_range(1)));
fprintf('High-frequency slope (T(s)): %.2f dB/decade\n', slope_high);

% T1(s)의 Bode 선도
figure;
[mag1, phase1, omega1] = bode(T1);
mag1 = squeeze(mag1); % 크기 응답
phase1 = squeeze(phase1); % 위상 응답

% Bode 선도 그리기
subplot(2, 1, 1);
semilogx(omega1, 20*log10(mag1)); % 크기 응답 (dB)
title('Bode Plot of T1(s)');
xlabel('Frequency (rad/s)');
ylabel('Magnitude (dB)');
grid on;

% 고주파수 영역에서 기울기 추정
high_freq_range_1 = omega1(omega1 > 10^2 & omega1 < 10^3);
high_mag_1 = mag1(omega1 > 10^2 & omega1 < 10^3);
slope_high_1 = (20 * log10(high_mag_1(end)) - 20 * log10(high_mag_1(1))) / (log10(high_freq_range_1(end)) - log10(high_freq_range_1(1)));
fprintf('High-frequency slope (T1(s)): %.2f dB/decade\n', slope_high_1);
```
![image](https://github.com/user-attachments/assets/315b2126-d5e8-431a-a9ee-ff407b1478ef)
![image](https://github.com/user-attachments/assets/776aeaac-c573-4a56-9aa9-3b2bdfd59cfe)
![image](https://github.com/user-attachments/assets/9eb48069-f59f-44d2-8682-66a83b858cf1)

(c)
```
% 전달함수 T(s)와 T1(s) 정의
s = tf('s');
T = 100*(s-1)/(s^2 + 25*s + 100);  % T(s)
T1 = 100*(s+1)/(s^2 + 25*s + 100); % T1(s)

% 공통 주파수 범위 설정
omega = logspace(-1, 3, 500); % 주파수 범위

% T(s)에서 크기 응답 계산
[mag_T, ~, omega_T] = bode(T, omega);
mag_T = squeeze(mag_T); % T(s) 크기 응답

% T1(s)에서 크기 응답 계산
[mag_T1, ~, omega_T1] = bode(T1, omega);
mag_T1 = squeeze(mag_T1); % T1(s) 크기 응답

% 첫 번째 그래프: T(s)의 Bode 크기선도
figure;
semilogx(omega_T, 20*log10(mag_T), 'b', 'LineWidth', 2); % T(s) 크기 응답
title('Bode Magnitude Response of T(s)');
xlabel('Frequency (rad/s)');
ylabel('Magnitude (dB)');
grid on;

% 두 번째 그래프: T1(s)의 Bode 크기선도
figure;
semilogx(omega_T1, 20*log10(mag_T1), 'r', 'LineWidth', 2); % T1(s) 크기 응답
title('Bode Magnitude Response of T1(s)');
xlabel('Frequency (rad/s)');
ylabel('Magnitude (dB)');
grid on;

```
![image](https://github.com/user-attachments/assets/925064e7-137a-425f-bfb4-5c15b8e690e9)
![image](https://github.com/user-attachments/assets/7a787f86-3aa6-46b3-a580-4caaf8ae3cc3)

(a)

```
% 상태공간 모델의 행렬 정의
A = [3 1; -1 2];
B = [1; 1/2];
C = [1 -2];
D = 0;

% 상태공간 모델을 전달함수로 변환
sys = ss(A, B, C, D);
G_s = tf(sys);  % 전달함수를 tf 객체로 계산

% 전달함수 식 형태로 출력
G_s
```
![image](https://github.com/user-attachments/assets/a751bbd1-a3df-4a42-a349-ec0c1862e23c)

(b)
```
% 상태공간 모델의 행렬 정의
A = [3 1; -1 2];
B = [1; 1/2];
C = [1 -2];
D = 0;

% 상태공간 모델을 전달함수로 변환
sys = ss(A, B, C, D);

% Bode 선도 그리기
figure;
bode(sys);
grid on;
title('Bode Plot of the System');
```
![image](https://github.com/user-attachments/assets/af90c152-302d-4285-bb13-b4a2b6b6eb6b)
![image](https://github.com/user-attachments/assets/10935f62-e3c2-43a1-bb18-b90c127e3574)

(a)
```
% 전달함수 정의
s = tf('s');
L = 1 / ((1 + 0.5*s)*(1 + 2*s));

% 주파수 범위 설정
omega = logspace(-1, 2, 500);  % 주파수 범위 (0.1 ~ 100)

% 전달함수의 주파수 응답 계산
[mag, phase, ~] = bode(L, omega);  % 크기와 위상 응답 계산

% 3차원 배열을 2차원으로 변환
mag = squeeze(mag);  % 크기 응답을 2차원 배열로 변환
phase = squeeze(phase);  % 위상 응답을 2차원 배열로 변환

% 극좌표선도 그리기
figure;
polarplot(phase*pi/180, mag, 'LineWidth', 2);  % 위상은 라디안 단위로 변환
title('Frequency Response of L(s) = 1 / ((1 + 0.5s)(1 + 2s))');
```
![image](https://github.com/user-attachments/assets/f31f0a2a-e273-432d-8e06-a822b24b5644)


(b)
```
% 전달함수 정의
s = tf('s');
L = 3 * (s^2 + 1.5*s + 1) / (s - 2)^2;

% 주파수 범위 설정
omega = logspace(-1, 2, 500);  % 주파수 범위 (0.1 ~ 100)

% 전달함수의 주파수 응답 계산
[mag, phase, ~] = bode(L, omega);  % 크기와 위상 응답 계산

% 3차원 배열을 2차원으로 변환
mag = squeeze(mag);  % 크기 응답을 2차원 배열로 변환
phase = squeeze(phase);  % 위상 응답을 2차원 배열로 변환

% 극좌표선도 그리기
figure;
polarplot(phase*pi/180, mag, 'LineWidth', 2);  % 위상은 라디안 단위로 변환
title('Frequency Response of L(s) = 3*(s^2 + 1.5s + 1) / (s - 2)^2');

```
![image](https://github.com/user-attachments/assets/313e93dd-db25-446b-8632-31e9fb6ef9df)


(c)
```
% 전달함수 정의
s = tf('s');
L = (s - 6) / (s^2 + 5*s + 6);

% 주파수 범위 설정
omega = logspace(-1, 2, 500);  % 주파수 범위 (0.1 ~ 100)

% 전달함수의 주파수 응답 계산
[mag, phase, ~] = bode(L, omega);  % 크기와 위상 응답 계산

% 3차원 배열을 2차원으로 변환
mag = squeeze(mag);  % 크기 응답을 2차원 배열로 변환
phase = squeeze(phase);  % 위상 응답을 2차원 배열로 변환

% 극좌표선도 그리기
figure;
polarplot(phase*pi/180, mag, 'LineWidth', 2);  % 위상은 라디안 단위로 변환
title('Frequency Response of L(s) = (s - 6) / (s^2 + 5s + 6)');

```
![image](https://github.com/user-attachments/assets/fb1ca6e4-5a6d-4f55-b3c6-5aeffd5739f9)


(d)
```
% 전달함수 정의
s = tf('s');
L = (s + 4) / (s^2 + 2*s + 4);

% 주파수 범위 설정
omega = logspace(-1, 2, 500);  % 주파수 범위 (0.1 ~ 100)

% 전달함수의 주파수 응답 계산
[mag, phase, ~] = bode(L, omega);  % 크기와 위상 응답 계산

% 3차원 배열을 2차원으로 변환
mag = squeeze(mag);  % 크기 응답을 2차원 배열로 변환
phase = squeeze(phase);  % 위상 응답을 2차원 배열로 변환

% 극좌표선도 그리기
figure;
polarplot(phase*pi/180, mag, 'LineWidth', 2);  % 위상은 라디안 단위로 변환
title('Frequency Response of L(s) = (s + 4) / (s^2 + 2s + 4)');

```
![image](https://github.com/user-attachments/assets/4dd68f7a-fb66-4d2f-a59f-ff01e419f899)

![image](https://github.com/user-attachments/assets/0195c46a-450a-4fdf-9cad-4711eab2ff64)
```
% 전달함수 정의
s = tf('s');

% 제어기, 밸브, 공정, 측정기의 전달함수
G_control = 2*s + 2;  % 제어기
G_valve = 1 / ((0.2*s + 1)*(s/30 + 1));  % 밸브
G_process = 1 / s;  % 공정
G_measurement = 100 / (s^2 + 10*s + 100);  % 측정기

% 피드백 구조에 따른 전달함수
G_total = (G_control * G_valve * G_process * G_measurement) / (1 + G_control * G_valve * G_process * G_measurement);

% 전달함수 출력
G_total
```
![image](https://github.com/user-attachments/assets/35b27dac-0a14-49aa-859c-142f04cbe1ff)
