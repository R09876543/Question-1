# Question-1
import numpy as np
import odespy
import matplotlib.pyplot as plt

def f(u, t):
    """Defines the system of ODEs."""
    x, v = u
    dxdt = v
    dvdt = -x
    return [dxdt, dvdt]

def main():
    X_0 = 1.0  # Initial position
    t0, t_end, dt = 0, 10, 0.1  # Start time, end time, and time step
    
    # Time points for the solution
    t_points = np.arange(t0, t_end + dt, dt)
    
    # Initial condition: [0, X_0]
    initial_condition = [0, X_0]
    
    # Create solver object (using Runge-Kutta method)
    solver = odespy.RK4(f)
    solver.set_initial_condition(initial_condition)
    
    # Solve the system
    u, t = solver.solve(t_points)
    
    # Plot results
    plt.figure(figsize=(10, 5))
    plt.plot(t, u[:, 0], label='x(t)', lw=2)
    plt.plot(t, u[:, 1], label='v(t)', lw=2)
    plt.xlabel('Time')
    plt.ylabel('Values')
    plt.legend()
    plt.title('Oscillating System')
    plt.grid()
    plt.show()

if __name__ == "__main__":
    main()
