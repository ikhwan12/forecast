Exponential smoothing state space model
======================
The methodology is fully automatic. The only required argument for ets is the time series. The model is chosen automatically if not specified.

```s
ets <- function(y, model="ZZZ", damped=NULL, alpha=NULL, beta=NULL, gamma=NULL, phi=NULL, additive.only=FALSE, lambda=NULL, biasadj=FALSE, lower=c(rep(0.0001, 3), 0.8), upper=c(rep(0.9999, 3), 0.98), opt.crit=c("lik", "amse", "mse", "sigma", "mae"), nmse=3, bounds=c("both", "usual", "admissible"), ic=c("aicc", "aic", "bic"), restrict=TRUE, allow.multiplicative.trend=FALSE, use.initial.values=FALSE, na.action = c("na.contiguous", "na.interp", "na.fail"), ...)
```

#### Parameter explanation:
* `y` = a numeric vector or time series of class `ts`
* `model` Usually a three-character string identifying method using the
framework terminology such as:
  1. The first letter denotes the error type (`A`, `M` or `Z`)
  2. The second denotes the trend type (`N`,`A`, `M` or `Z`)
  3. the third letter denotes the season type (`N`,`A`, `M` or `Z`)

  In all cases, `N`=none, `A`=additive, `M`=multiplicative and `Z`=automatically selected. So, for example, `ANN` is simple exponential smoothing with additive errors, `MAM` is multiplicative Holt-Winters' method with multiplicative errors, and so on.
* `damped` If TRUE, use a damped trend (either additive or multiplicative). If NULL, both damped and non-damped trends will be tried and the best model (according to the information criterion `ic`) returned.
* `alpha` Value of alpha. If NULL, it is estimated.
* `beta` Value of beta. If NULL, it is estimated.
* `gamma` Value of gamma. If NULL, it is estimated.
* `phi` Value of phi. If NULL, it is estimated.
* `additive.only` If TRUE, will only consider additive models. Default is FALSE.
* `lambda` Box-Cox transformation parameter. If `lambda="auto"` then a transformation is automatically selected using `BoxCox.lambda`. The transformation is ignored if NULL. Otherwise, data transformed before model is estimated. When `lambda` is specified, `additive.only` is set to `TRUE`.
* `lower` Lower bounds for the parameters (alpha, beta, gamma, phi)
* `upper` Upper bounds for the parameters (alpha, beta, gamma, phi)
* `opt.crit` Optimization criterion. One of "mse" (Mean Square Error), "amse" (Average MSE over first \code{nmse} forecast horizons), "sigma" (Standard deviation of residuals), "mae" (Mean of absolute residuals), or "lik" (Log-likelihood, the default).
* `nmse` Number of steps for average multistep MSE (1<=`nmse` <=30).
* `bounds` Type of parameter space to impose: `"usual" ` indicates all parameters must lie between specified lower and upper bounds; `"admissible"` indicates parameters must lie in the admissible space; `"both"` (default) takes the intersection of these regions.
* `ic` Information criterion to be used in model selection.
* `restrict` If `TRUE` (default), the models with infinite variance will not be allowed.
* `allow.multiplicative.trend` If `TRUE`, models with multiplicative trend are allowed when searching for a model. Otherwise, the model space excludes them. This argument is ignored if a multiplicative trend model is explicitly requested (e.g., using `model="MMN"`).
* `use.initial.values` If `TRUE` and `model` is of class `"ets"`, then the initial values in the model are also not re-estimated.
* `na.action` A function which indicates what should happen when the data contains NA values. By default, the largest contiguous portion of the time-series will be used.

## Installation

You can install the **development** version from
[Github](https://github.com/ikhwan12/forecast)

```s
# install.packages("remotes")
remotes::install_github("ikhwan12/forecast")
```

## Usage

```s
library(forecast)
library(ggplot2)

# ETS forecasts
fit <- ets(bss, model = "MNA")
plot(forecast(fit))

#See the prediction result
res = forecast(fit)
res
```
