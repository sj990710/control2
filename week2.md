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
![image](https://github.com/user-attachments/assets/7ac416e6-9772-4fa3-bbd3-53c6c32061a3)

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
![image](https://github.com/user-attachments/assets/fc699c59-ea07-422c-96a5-f2b3a398f5f6)

![image](https://github.com/user-attachments/assets/bd938552-55b6-4491-94b6-63e8bc848e5a)
![image](https://github.com/user-attachments/assets/e684ca11-5cf6-472d-8785-dd6bbb1e0413)

