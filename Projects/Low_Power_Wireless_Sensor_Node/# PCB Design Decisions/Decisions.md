# PCB Design Decisions

| Design Decision | Reason |
|---------------|---------|
| PMIC placed near USB-C connector | Minimized power-path length and voltage drop |
| BM15M placed centrally | Reduced routing complexity and signal lengths |
| Programming header placed at board edge | Easier debugging and firmware updates |
| Ground copper pour used | Improved return-current paths and reduced noise |
| Short routing paths used | Improved signal integrity and reduced EMI susceptibility |
| Smooth trace routing preferred | Improved readability and manufacturing consistency |
| Modular sensor connectors provided | Allowed future sensor expansion without PCB redesign |
| Compact board dimensions selected | Reduced overall system size while maintaining manufacturability |
