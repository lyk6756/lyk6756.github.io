---
layout: article
title: "Consistent Unit Systems in FEA"
key: 20161201
lang: en
tags: ABAQUS
---

| Symbol | Quantity | Dimension | N‐m SI | N‐mm SI | in‐lb System | ft‐lb System |
|:------:|:--------:|:---------:|------:|-------:|------------:|------------:|
| $$l$$ | length | $$L$$ | meter($$\text{m}$$) | millimeter($$\text{mm}$$) | inch($$\text{in}$$) | foot($$\text{ft}$$) |
| $$m$$ | mass | $$M$$ | kilogram($$\text{kg}$$) | tonne($$\text{t}$$, $$10^3\text{kg}$$) | snail = 386.2 "lb mass" | [slug](https://en.wikipedia.org/wiki/Slug_(mass)) = 32.19 "lb mass" |
| $$F$$ | force | $$MLT^{-2}$$ | Newton($$\text{N}$$) | Newton($$\text{N}$$) | pound-force($$\text{lbf}$$) | pound-force($$\text{lbf}$$) |
| $$v$$ | velocity | $$LT^{-1}$$ | $$\text{m/s}$$ | $$\text{mm/s}$$ | $$\text{in/s}$$ | $$\text{ft/s}$$ |
| $$a$$ | acceleration | $$LT^{-2}$$ | $$\text{m/s}^2$$ | $$\text{mm/s}^2$$ | $$\text{in/s}^2$$ | $$\text{ft/s}^2$$ |
| $$g$$ | gravity | $$LT^{-2}$$ | $$9.8\text{m/s}^2$$ | $$9.8\times10^3\text{mm/s}^2$$ | $$386.2\text{in/s}^2$$ | $$32.19\text{ft/s}^2$$ |
| $$\sigma/p$$ | stress/pressure | $$ML^{-1}T^{-2}$$ | Pascal($$\text{Pa}$$, $$\text{N/m^2}$$) | MegaPascal($$\text{MPa}$$, $$\text{N/mm^2}$$) | $$\text{psi}$$, $$\text{lbf/in}^2$$ | $$\text{lbf/ft}^2$$ |
| $$\rho$$ | density | $$ML^{-3}$$ | $$\text{kg/m}^3$$ | $$\text{t/mm}^3$$ | $$\text{snails/in}^3$$ | $$\text{slugs/ft}^3$$ |
| $$E/W/M$$ | energy/work/moment | $$ML^2T^{-2}$$ | Joule($$\text{J}$$, $$\text{N}\cdot\text{m}$$) | milliJoule($$\text{mJ}(10^{-3}\text{J})$$, $$\text{N}\cdot\text{mm}$$) | $$\text{lbf}\cdot\text{in}$$ | $$\text{lbf}\cdot\text{ft}$$ |

## Discuss on Imperial Units

It  is critical to  note that  a  pound  is  **not**  a  unit  of  mass  for  engineers  and  should  not  be  used  as  a unit of mass. That is to say:

**A pound is a unit of force.**

Not so obvious is that mass is now in units of "12 x slugs".  Although some have named this mass unit the "slinch" or "blob", we prefer the colloquially applied name, the "snail".

---

## Further reading

* [International System of Units - wikipedia](https://en.wikipedia.org/wiki/International_System_of_Units)
* [Conversion of units - wikipedia](https://en.wikipedia.org/wiki/Conversion_of_units)
* [Consistent Engineering Units In Finite Element Analysis - EnDuraSim](http://www.endurasim.com.au/wp-content/uploads/2015/02/EnDuraSim-Engineering-Units.pdf)
* [Units - Abaqus](https://abaqus-docs.mit.edu/2017/English/SIMACAEGSARefMap/simagsa-c-absunits.htm)
* [Consistent units — LS-DYNA Support](http://www.dynasupport.com/howtos/general/consistent-units)
* [Consistent Units - Altair University](http://www.altairuniversity.com/wp-content/uploads/2012/04/Student_Guide_55-57.pdf)
* [有限元计算中的单位制 - Glulam的博客](http://blog.sina.com.cn/s/blog_462c6348010005ox.html)
