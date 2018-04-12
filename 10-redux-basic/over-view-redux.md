# Redux の概要

[https://codesandbox.io/s/kk2vx81z13](https://codesandbox.io/s/kk2vx81z13)![](/assets/redux.001.jpeg)  
![](/assets/redux.002.jpeg)

- Redux は state の管理(保持と変更)を担当する。
- Redux の ** store ** がそれを主に担当する。
- ** store ** は 「一つ前の state, ** dispatch ** された ** action **, ** reducer **」を用いて、新しい state を生成し、これで自分自身の state を上書きすることで state を更新する。
- redux で管理した state を変更するためには、かならず ** aciton ** ** dispatch ** することで行うこと。(`this.setState()`は使わない)
- ** reducer ** は 「一つ前の state, ** dispatch ** された ** action **」を元に新しい state を生成するための ** 「関数」 **。

      
![](/assets/redux.003.jpeg)

