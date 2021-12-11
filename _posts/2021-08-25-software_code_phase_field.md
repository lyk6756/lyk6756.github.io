---
layout: article
title:  "使用有限元方法求解相场断裂模型的主要软件及开源代码"
author: 李宇琨
key: 20210825
lang: en
tags: Phase-field MATLAB Fortran Python ABAQUS
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: "https://dm2305files.storage.live.com/y4m8dk_trIXJZ-XVzYrAG3o0qDHYnPkFCsB6-SXosExTy6ZjBSLs575rE5hyfFaHxen1Am06tqpdKc40uR2T9g7Wl-nvRcOVl0toamKKhL35pXR3XdPq3mmW19lLmqrZXrpmRU6g-8Oyy8KmVgZZ3031RA3WUXgT-_09koO0B557r3jFoBgMFdug8kxwJaItFBf?width=1362&height=1071&cropmode=none"
---

### Notable software packages and available codes that implement the finite element method for solving phase-field fracture (PFF) models

|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|
| Software                           | Language interface | Price      | Available codes for PFF                                                               |
|------------------------------------|--------------------|------------|---------------------------------------------------------------------------------------|
| [MATLAB][MATLAB]                   | MATLAB             | Commercial | Biner[^Biner]                                                                         |
|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|
| [mef90/vDef][mef90/vDef][^mef90]   | Fortran            | Free       | [Bourdin][Bourdin][^Bourdin]                                                          |
|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|
| [JIVE][JIVE][^JIVE]                | C++                | Free       | [Nguyen][Nguyen][^Nguyen]                                                             |
|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|
| [deal.II][deal][^deal]             | C++                | Free       | [Heister][Heister][^Heister]                                                          |
|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|
| [FEniCS][FEniCS][^FEniCS]          | C++ & Python       | Free       | [Farrell][Farrell][^Farrell], [Ratna][Ratna][^Ratna], [Martínez-Pañeda][Martínez-Pañeda][^Martinez-Paneda1]         |
|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|
| [COMSOL][COMSOL]                   | MATLAB             | Commercial | [Zhou et al.][Zhou][^Zhou], [Wu][Wu1][^Wu1]                                           |
|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|
| [ABAQUS][ABAQUS]                   | Fortran            | Commercial | [Molnár][Molnár][^Molnar], [Fang et al.][Fang][^Fang], [Seles et al.][Seles][^Seles], [Martínez-Pañeda][Martínez-Pañeda][^Martinez-Paneda2], [Wu][Wu2][^Wu2] |
|------------------------------------+--------------------+------------+---------------------------------------------------------------------------------------|

[MATLAB]: https://www.mathworks.com/products/matlab.html "MATLAB"
[mef90/vDef]: https://github.com/bourdin/mef90 "mef90/vDef"
[Bourdin]: https://github.com/bourdin/mef90 "Bourdin"
[JIVE]: https://software.dynaflow.com/jive/ "JIVE"
[Nguyen]: https://github.com/vinhphunguyen/ofeFRAC "Nguyen"
[deal]: https://www.dealii.org/ "deal"
[Heister]: https://github.com/tjhei/cracks "Heister"
[FEniCS]: https://fenicsproject.org/ "FEniCS"
[Farrell]: https://bitbucket.org/pefarrell/varfrac-solvers "Farrell"
[Ratna]: https://home.iitm.ac.in/ratna/codes/phasefield/ "Ratna"
[Martínez-Pañeda]: https://www.empaneda.com/codes/ "Martínez-Pañeda"
[COMSOL]: https://www.comsol.com/ "COMSOL"
[Zhou]: https://sourceforge.net/projects/phasefieldmodelingcomsol/ "Zhou"
[Wu1]: https://github.com/jianyingwu/pfczm-comsol "Wu1"
[ABAQUS]: http://www.abaqus.com/ "ABAQUS"
[Molnár]: http://molnar-research.com/publication.html "Molnár"
[Fang]: https://doi.org/10.17632/9n6rhvmjjn "Fang"
[Seles]: https://doi.org/10.17632/p77tsyrbx2 "Seles"
[Wu2]: https://github.com/jianyingwu/pfczm-abaqus "Wu2"

### References

[^Biner]: [Biner, S. Bulent. Programming phase-field modeling. Springer International Publishing, 2017.](https://doi.org/10.1007/978-3-319-41196-5)

[^mef90]: [Bourdin, kumiori, cmaurini, et al. bourdin/mef90: Full rewrite of the assembly routines leveraging OO features of F2008. Zenodo, 2020.](https://doi.org/10.5281/zenodo.3242131)

[^Bourdin]: [Bourdin, B., Francfort, G., and Marigo, J.-J. (2000). Numerical experiments in revisited brittle fracture. J. Mech. Phys. Solids, 48(4):797–826.](http://doi.org/10.1016/S0022-5096(98)00034-9)

    [Bourdin, B. (2007). Numerical implementation of a variational formulation of quasi-static brittle fracture. Interfaces Free Bound., 9:411–430.](http://doi.org/10.4171/IFB/171)

    [Bourdin, B., Francfort, G., and Marigo, J.-J. (2008). The variational approach to fracture. J. Elasticity, 91(1-3):1–148.](http://doi.org/10.1007/s10659-007-9107-3)

[^JIVE]: [Nguyen-Thanh, Chi, et al. Jive: an open source, research-oriented C++ library for solving partial differential equations. Advances in Engineering Software 150 (2020): 102925.](https://doi.org/10.1016/j.advengsoft.2020.102925)

[^Nguyen]: [Wu, Jian-Ying, et al. Computational modeling of localized failure in solids: XFEM vs PF-CZM. Computer Methods in Applied Mechanics and Engineering 345 (2019): 618-643.](https://doi.org/10.1016/j.cma.2018.10.044)

    [MANDAL T K, NGUYEN V P, HEIDARPOUR A. Phase field and gradient enhanced damage models for quasi-brittle failure: A numerical comparative study. Engineering Fracture Mechanics, 2019, 207: 48-67.](https://doi.org/10.1016/j.engfracmech.2018.12.013)

    [MANDAL T K, NGUYEN V P, WU J Y. Length scale and mesh bias sensitivity of phase-ﬁeld models for brittle and cohesive fracture. Engineering Fracture Mechanics, 2019, 217: 106532.](https://doi.org/10.1016/j.engfracmech.2019.106532.)

    [MANDAL T K, NGUYEN V P, WU J Y. Comparative study of phase-ﬁeld damage models for hydrogen assisted cracking. Theoretical and Applied Fracture Mechanics, 2021, 111: 102840.](https://doi.org/10.1016/j.tafmec.2020.102840)

[^deal]: [ARNDT D, BANGERTH W, BLAIS B, et al. The deal.II library, version 9.2. Journal of Numerical Mathematics, 2020, 28(3): 131-146.](https://doi.org/10.1515/jnma-2020-0043)

[^Heister]: [HEISTER T, WHEELER M F, WICK T. A primal-dual active set method and predictor-corrector mesh adaptivity for computing fracture propagation using a phase-ﬁeld approach. Computer Methods in Applied Mechanics and Engineering, 2015, 290: 466-495.](https://doi.org/10.1016/j.cma.2015.03.009)

    [HEISTER T, WICK T. Parallel solution, adaptivity, computational convergence, and open-source code of 2d and 3d pressurized phase-ﬁeld fracture problems. PAMM, 2018, 18(1).](https://doi.org/10.1002/pamm.201800353)

[^FEniCS]: [ALNÆS M S, BLECHTA J, HAKE J, et al. The fenics project version 1.5. Archive of Numerical Software, 2015, 3(100).](https://doi.org/10.11588/ans.2015.100.20553)

[^Farrell]: [FARRELL P, MAURINI C. Linear and nonlinear solvers for variational phase-ﬁeld models of brittle fracture. International Journal for Numerical Methods in Engineering, 2016, 109(5): 648-667.](https://doi.org/10.1002/nme.5300)

[^Ratna]: [HIRSHIKESH, NATARAJAN S, ANNABATTULA R K. A FEniCS implementation of the phase ﬁeld method for quasi-static brittle fracture. Frontiers of Structural and Civil Engineering, 2018, 13(2): 380-396.](https://doi.org/10.1007/s11709-018-0471-9)

[^Martinez-Paneda1]: [HIRSHIKESH, NATARAJAN S, ANNABATTULA R K, et al. Phase ﬁeld modelling of crack propagation in functionally graded materials. Composites Part B: Engineering, 2019, 169: 239-248.](https://doi.org/10.1016/j.compositesb.2019.04.003)

[^Zhou]: [ZHOU S, RABCZUK T, ZHUANG X. Phase ﬁeld modeling of quasi-static and dynamic crack propagation: COMSOL implementation and case studies. Advances in Engineering Software, 2018, 122: 31-49.](https://doi.org/10.1016/j.advengsoft.2018.03.012)

[^Wu1]: [WU J Y, CHEN W X. Phase-ﬁeld modeling of electromechanical fracture in piezoelectric solids: Analytical results and numerical simulations. Computer Methods in Applied Mechanics and Engineering, 2021.](https://doi.org/10.1016/j.cma.2021.114125)

    [CHEN W X, WU J Y. Phase-field cohesive zone modeling of multi-physical fracture in solids and the open-source implementation in Comsol Multiphysics. Theoretical and Applied Fracture Mechanics, 2022, 117: 103153](https://doi.org/10.1016/j.tafmec.2021.103153)

[^Molnar]: [MOLNÁR G, GRAVOUIL A. 2d and 3d abaqus implementation of a robust staggered phase-ﬁeld solution for modeling brittle fracture. Finite Elements in Analysis and Design, 2017, 130: 27-38.](https://doi.org/10.1016/j.finel.2017.03.002)

    [MOLNÁR G, GRAVOUIL A, SEGHIR R, et al. An open-source abaqus implementation of the phase-ﬁeld method to study the eﬀect of plasticity on the instantaneous fracture toughness in dynamic crack propagation. Computer Methods in Applied Mechanics and Engineering, 2020, 365: 113004.](https://doi.org/10.1016/j.cma.2020.113004)

[^Fang]: [FANG J, WU C, RABCZUK T, et al. Phase ﬁeld fracture in elasto-plastic solids: Abaqus implementation and case studies. Theoretical and Applied Fracture Mechanics, 2019, 103: 102252.](https://doi.org/10.1016/j.tafmec.2019.102252)

[^Seles]: [SELEŠ K, LESIČAR T, TONKOVIĆ Z, et al. A residual control staggered solution scheme for the phase-ﬁeld modeling of brittle fracture. Engineering Fracture Mechanics, 2019, 205: 370-386.](https://doi.org/10.1016/j.engfracmech.2018.09.027)

[^Martinez-Paneda2]: [KRISTENSEN P K, MARTÍNEZ-PAÑEDA E. Phase ﬁeld fracture modelling using quasi-newton methods and a new adaptive step scheme. Theoretical and Applied Fracture Mechanics, 2020, 107: 102446.](https://doi.org/10.1016/j.tafmec.2019.102446)

    [MARTÍNEZ-PAÑEDA E, GOLAHMAR A, NIORDSON C F. A phase ﬁeld formulation for hydrogen assisted cracking. Computer Methods in Applied Mechanics and Engineering, 2018, 342: 742-761.](https://doi.org/10.1016/j.cma.2018.07.021)

    [CUI C, MA R, MARTÍNEZ-PAÑEDA E. A phase ﬁeld formulation for dissolutiondriven stress corrosion cracking. Journal of the Mechanics and Physics of Solids, 2021, 147: 104254.](https://doi.org/10.1016/j.jmps.2020.104254)

    [NAVIDTEHRANI Y, BETEGÓN C, MARTÍNEZ-PAÑEDA E. A uniﬁed abaqus implementation of the phase ﬁeld fracture method using only a user material subroutine. Materials, 2021, 14(8): 1913.](https://doi.org/10.3390/ma14081913)

    [NAVIDTEHRANI Y, BETEGÓN C, MARTÍNEZ-PAÑEDA E. A simple and robust abaqus implementation of the phase ﬁeld fracture method. Applications in Engineering Science, 2021, 6: 100050.](https://doi.org/10.1016/j.apples.2021.100050)
    
[^Wu2]: [WU J Y, HUANG Y, NGUYEN V P. On the BFGS monolithic algorithm for the uniﬁed phase ﬁeld damage theory. Computer Methods in Applied Mechanics and Engineering, 2020, 360: 112704.](https://doi.org/10.1016/j.cma.2019.112704)

    [WU J Y, HUANG Y. Comprehensive implementations of phase-ﬁeld damage models in abaqus. Theoretical and Applied Fracture Mechanics, 2020, 106: 102440.](https://doi.org/10.1016/10.1016/j.tafmec.2019.102440)
