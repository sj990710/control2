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
