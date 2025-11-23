# Zero-Parameter Two-Field Cosmology

Complete derivation of cosmological constants from first principles using the Anti-Entropic Principle (AEP).

## 📖 Paper
- **Location**: `paper/main.tex`
- **Compiled PDF**: [Download here](paper/output.pdf) *(upload after compilation)*

## 🎯 Key Results
- Resolves Hubble tension: $H_0 = 73.63 \pm 0.15$ km/s/Mpc
- Resolves $S_8$ tension: $S_8 = 0.758 \pm 0.008$  
- **Zero free parameters** - all determined from first principles
- Excellent fit to Planck CMB data ($\chi^2$/dof = 1.020)

## 📁 Repository Structure
aep-cosmology/
├──paper/           # LaTeX source and compiled PDF
├──code/            # Numerical implementations
├──data/            # Supporting data files
├──README.md        # This file
└──LICENSE          # MIT License


## 🚀 Quick Start
1. **Compile paper**: Use any LaTeX compiler on `paper/main.tex`
2. **Run analysis**: See code directories for specific implementations

## 🔬 Code Overview
- `code/parameter_determination/` - Algorithm implementations
- `code/class_modifications/` - Modified CLASS code (cosmology solver)

## 📝 Citation
If you use this work, please cite:
```bibtex
@article{devine2024zeroparameter,
  title={A Zero-Parameter Two-Field Cosmology: Complete Derivation of Cosmological Constants from First Principles},
  author={Devine, Scott},
  journal={Preprint},
  year={2024}
}

📞 Contact

· Scott Devine: scottdevine01@gmail.com
· Issues: Use GitHub Issues for questions/discussions


### B. Parameter Solver Code
Create: `code/parameter_determination/parameter_solver.py`

**Paste this placeholder:**
```python
"""
Parameter Determination Algorithm for AEP Two-Field Cosmology

Implements Algorithm 1 from the paper: hierarchical optimization
to determine the six parameters {g, λ, κ, v_χ, λ_χ, γ} from
empirical coherence scales.
"""

import numpy as np
from scipy.optimize import root
from scipy import constants as const

class AEPParameterSolver:
    """
    Solves for AEP two-field cosmology parameters from empirical scales.
    """
    
    def __init__(self):
        # Physical constants
        self.M_P = 2.435e18  # Planck mass in eV
        self.c = const.c
        self.hbar = const.hbar
        
        # Empirical scales (from paper)
        self.rho_Lambda = (2.4e-3)**4  # Dark energy scale in eV^4
        self.a0 = 1.20e-10  # MOND scale in m/s^2
        self.Rc = 3.09e19   # Structure transition scale in m
        
    def determine_g_from_empirical(self):
        """Determine g parameter from empirical scale a0"""
        numerator = self.c**12
        denominator = self.a0**4 * self.hbar**4 * self.M_P**4 * 3
        g = (numerator / denominator)**(1/3)
        return g
    
    def determine_parameters(self):
        """Main parameter determination algorithm"""
        print("Running AEP Parameter Determination...")
        
        # Step 1: Determine g from empirical scale
        g = self.determine_g_from_empirical()
        
        # Step 2: Determine λ from theoretical consistency
        lambda_param = g**2 / 3
        
        # Step 3: Determine X_min from attractor condition
        X_min = -1 / (4 * g)
        
        print(f"Initial parameters:")
        print(f"g = {g:.6e}")
        print(f"λ = {lambda_param:.6e}")
        print(f"X_min = {X_min:.6e}")
        
        # Placeholder for iterative solution of remaining parameters
        # This would implement the Newton-Raphson method from Algorithm 1
        
        return {
            'g': g,
            'lambda': lambda_param,
            'X_min': X_min,
            'kappa': 1.997e-4,  # From paper - would be solved iteratively
            'v_chi': 1.002e-29,
            'lambda_chi': 9.98e-11,
            'gamma': 2.00e-2
        }

if __name__ == "__main__":
    solver = AEPParameterSolver()
    params = solver.determine_parameters()
    
    print("\nFinal AEP Parameters:")
    for key, value in params.items():
        print(f"{key:12} = {value:.6e}")
