>> %% Parameters
L = 10; % Length of heat exchanger (m)
N = 100; % Discretization points
xspan = linspace(0,L,N);
T_hot_in = 150; 
T_cold_in = 30;
m_dot_hot = 1;
m_dot_cold = 1.5;
C_p_hot = 4180; % J/kg·°C
C_p_cold = 4180;
U = 500; % W/m²·°C

% Initial conditions
T0 = [T_hot_in; T_cold_in];

%% Solve ODEs using anonymous function
[x,T] = ode45(@(x,T) [-U*(T(1)-T(2))/(m_dot_hot*C_p_hot); 
                      U*(T(1)-T(2))/(m_dot_cold*C_p_cold)], xspan, T0);

% Extract outlet temperatures
T_hot_out = T(end,1);
T_cold_out = T(end,2);

%% Compute temperature gradients
dTdx_hot = gradient(T(:,1), x);   
dTdx_cold = gradient(T(:,2), x);  

%% Plot temperature profiles
figure;
plot(x,T(:,1),'r','LineWidth',2); hold on;
plot(x,T(:,2),'b','LineWidth',2);
xlabel('Length along heat exchanger (m)');
ylabel('Temperature (°C)');
title('Counter-Flow Heat Exchanger Temperature Profiles');
legend('Hot fluid','Cold fluid');
grid on;

%% Plot temperature gradients
figure;
plot(x,dTdx_hot,'r','LineWidth',2); hold on;
plot(x,dTdx_cold,'b','LineWidth',2);
xlabel('Length along heat exchanger (m)');
ylabel('Temperature Gradient (°C/m)');
title('Temperature Gradients Along Heat Exchanger');
legend('Hot fluid','Cold fluid');
grid on;

%% Heatmap (pseudo-contour) of temperature
figure;
T_matrix = [T(:,1), T(:,2)]'; % 2xN matrix for hot/cold fluids
imagesc(x, [1 2], T_matrix); 
colormap(jet); colorbar;
yticks([1 2]); yticklabels({'Hot fluid','Cold fluid'});
xlabel('Length along heat exchanger (m)');
ylabel('Fluid');
title('Temperature Distribution Heatmap');

%% Display outlet temperatures
fprintf('Outlet temperature of hot fluid: %.2f °C\n', T_hot_out);
fprintf('Outlet temperature of cold fluid: %.2f °C\n', T_cold_out);

Outlet temperature of hot fluid: 87.81 °C
Outlet temperature of cold fluid: 71.46 °C
