# 背景
有限要素法の時間積分にはNewmark-β法を使用するのが一般的です。一方、接触問題などのように数値的な減衰が必要な際は[Hilber Hughes Taylor (HHT) scheme](https://escholarship.org/uc/item/18z548gt)が使用されることがあります。本記事ではこの手法を実装するための定式化を説明します。

# 定式化

運動方程式は次式で表されます。

```math
M\ddot{u}+C\dot{u}+K{u}=F
```

ここで、uは変位、Mは質量行列、Cは減衰行列、Kは剛性行列を表します。ここで、時間ステップが$n+1$ステップ目の運動方程式を考えます。

```math
M\ddot{u}_{n+1}+C\dot{u}_{n+1}+Ku_{n+1}=F_{n+1}
```

速度項と変位項を以下のようにするのがHHT法のアイディアです。

```math
M\ddot{u}_{n+1}+C\dot{u}'_{n+1}+Ku'_{n+1}=F_{n+1}
```

ただし、

```math
\begin{align}
\dot{u}'_{n+1} &= \left(1+\alpha\right)\dot{u}_{n+1}-\alpha \dot{u}_{n}\\
u'_{n+1} &= \left(1+\alpha\right){u}_{n+1}-\alpha{u}_{n} 
\end{align}
```

であり、Newmark-$\beta$法と同様に$n+1$ステップの変位と速度を次式で求めます。

```math
\begin{align}
\dot{u}_{n+1} &= \dot{u}_{n} + \Delta t \left(\left(1-\gamma\right)\ddot{u}_{n}+\gamma\ddot{u}_{n+1}\right) \\
u_{n+1} &= u_{n} + \Delta t \dot{u}_{n} + \Delta t^2 \left(\left(\dfrac{1}{2}-\beta\right) \ddot{u}_{n}+\beta\ddot{u}_{n+1}\right)
\end{align}
```

$n$ステップの状態量から、$n+1$ステップの加速度を計算するには以下の式を使用します。

```math
M'\ddot{u}_{n+1}=F_{n+1}-C\dot{u}''_{n+1}-K{u}''_{n+1}
```

ただし、

```math
\begin{align}
M' &= M-\left(1+\alpha\right)\Delta t\gamma C-\left(1+\alpha\right)\Delta t^2\beta K \\
\dot{u}''_{n+1} &= \dot{u}_{n} + \left(1+\alpha\right)\Delta t \left(1-\gamma\right)\ddot{u}_{n} \\
u''_{n+1} &= u_{n} + \Delta t \dot{u}_{n} + \left(1+\alpha\right)\Delta t^2 \left(\dfrac{1}{2}-\beta\right) \ddot{u}_{n}
\end{align}
```

この式を計算した後、先程の式で$n+1$ステップの変位と速度を計算します。

# 実装
