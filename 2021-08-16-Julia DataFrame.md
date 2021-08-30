```julia
using CSV, DataFrames
```


```julia
ENV["LINES"] = 5;
ENV["COLUMNS"] = 1000;
```

# 데이터프레임 만들기 Construction of DataFrame

Julia Datafame을 직접 만드는 방법은 pandas처럼 여러 가지가 있는데 아래처럼 column vector를 keyword 인자로 전달해 주는 방법이 가장 쓸만 해 보인다. pandas에서 주로 쓰던 방법이랑도 비슷하고.


```julia
df = DataFrame(A = 1:4, B = ["M", "F", "F", "M"])
```




<div class="data-frame"><p>4 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td></tr><tr><th>2</th><td>2</td><td>F</td></tr><tr><th>3</th><td>3</td><td>F</td></tr><tr><th>4</th><td>4</td><td>M</td></tr></tbody></table></div>



컬럼 이름 아래에 컬럼의 데이터 타입이 같이 표시된다.  
아무 인자도 전달하지 않으면 빈 데이터프레임이 만들어진다.


```julia
DataFrame()
```




<div class="data-frame"><p>0 rows × 0 columns</p><table class="data-frame"><thead><tr><th></th></tr><tr><th></th></tr></thead><tbody></tbody></table></div>



어떤 프로세스를 거쳐서 결과적으로 나오는 data들은 보통 table 형태를 많이 취하게 되는데, 그에 해당하는 것들이 Julia에는 array라던가 matrix라는 데이터 타입이다.
이들을 DataFrame 함수한테 인자로 주면 만들어진다. 2번째 인자로 vector를 주면 그것으로 column 이름을 만든다.

# 데이터를 읽어서 데이터프레임 만들기 Import and export data

CSV를 비롯한 text file들을 읽기 위해서 CSV.jl 패키지를 사용해야 한다.  
사용된 인자를 유심히 봐두기 바란다.


```julia
using CSV
```


```julia
DataFrame(CSV.File("german_credit_data.csv"))
```




<div class="data-frame"><p>1,000 rows × 10 columns</p><table class="data-frame"><thead><tr><th></th><th>Column1</th><th>Age</th><th>Sex</th><th>Job</th><th>Housing</th><th>Saving accounts</th><th>Checking account</th><th>Credit amount</th><th>Duration</th><th>Purpose</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="String">String</th><th title="Int64">Int64</th><th title="String">String</th><th title="String">String</th><th title="String">String</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>0</td><td>67</td><td>male</td><td>2</td><td>own</td><td>NA</td><td>little</td><td>1169</td><td>6</td><td>radio/TV</td></tr><tr><th>2</th><td>1</td><td>22</td><td>female</td><td>2</td><td>own</td><td>little</td><td>moderate</td><td>5951</td><td>48</td><td>radio/TV</td></tr><tr><th>3</th><td>2</td><td>49</td><td>male</td><td>1</td><td>own</td><td>little</td><td>NA</td><td>2096</td><td>12</td><td>education</td></tr><tr><th>4</th><td>3</td><td>45</td><td>male</td><td>2</td><td>free</td><td>little</td><td>little</td><td>7882</td><td>42</td><td>furniture/equipment</td></tr><tr><th>5</th><td>4</td><td>53</td><td>male</td><td>2</td><td>free</td><td>little</td><td>little</td><td>4870</td><td>24</td><td>car</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table></div>




```julia
german = CSV.read("german_credit_data.csv", DataFrame, delim=",", copycols=true) 
```




<div class="data-frame"><p>1,000 rows × 10 columns</p><table class="data-frame"><thead><tr><th></th><th>Column1</th><th>Age</th><th>Sex</th><th>Job</th><th>Housing</th><th>Saving accounts</th><th>Checking account</th><th>Credit amount</th><th>Duration</th><th>Purpose</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="String">String</th><th title="Int64">Int64</th><th title="String">String</th><th title="String">String</th><th title="String">String</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>0</td><td>67</td><td>male</td><td>2</td><td>own</td><td>NA</td><td>little</td><td>1169</td><td>6</td><td>radio/TV</td></tr><tr><th>2</th><td>1</td><td>22</td><td>female</td><td>2</td><td>own</td><td>little</td><td>moderate</td><td>5951</td><td>48</td><td>radio/TV</td></tr><tr><th>3</th><td>2</td><td>49</td><td>male</td><td>1</td><td>own</td><td>little</td><td>NA</td><td>2096</td><td>12</td><td>education</td></tr><tr><th>4</th><td>3</td><td>45</td><td>male</td><td>2</td><td>free</td><td>little</td><td>little</td><td>7882</td><td>42</td><td>furniture/equipment</td></tr><tr><th>5</th><td>4</td><td>53</td><td>male</td><td>2</td><td>free</td><td>little</td><td>little</td><td>4870</td><td>24</td><td>car</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table></div>



데이터프레임 df를 경로 output에 CSV file로 출력할 때는 다음과 같이 쓴다.
```julia
CSV.write(output, df)
```

다른 형태의 파일들은 다음을 참조해서 작업하면 된다.
- Apache Arrow (including Feather v2): Arrow.jl
- Apache Feather (v1): Feather.jl
- Apache Avro: Avro.jl
- JSON: JSONTables.jl
- Parquet: Parquet.jl
- Stata, SPSS, and SAS: StatFiles.jl
- Microsoft Excel (XLSX): XLSX.jl

인터넷 사이트의 내용을 읽어들일 때는 다음과 같이 CSV와 HTTP 패키지를 같이 이용해야 한다.  

```Julia
using HTTP

resp = HTTP.request("GET",
"https://data.cityofnewyork.us/api/views/kku6-nxdu/rows.csv?accessType=DOWNLOAD"
)
df = CSV.read(IOBuffer(String(resp.body)), DataFrame)
```

# 데이터프레임 보기  Insights from dataframe

데이터프레임이 어떻게 생겼는지는 `size` 함수를 통해 알 수 있다.  pandas의 `df.shape`이 떠오른다.  Python은 class를 사용하고 Julia는 함수를 사용하는 경향이 있나 보다.


```julia
size(df)
```




    (4, 2)




```julia
size(df, 1)
```




    4




```julia
size(df)[2]
```




    2



데이터프레임의 column 이름은 `names` 함수를 통해 얻을 수 있다. 문자열 형태로 나타난다. pandas의 `df.columns`와 같다.


```julia
names(df)
```




    2-element Vector{String}:
     ⋮



Symbol 형태로 column 이름을 얻으려면 `porpertynames` 함수를 사용한다.


```julia
propertynames(df)
```




    2-element Vector{Symbol}:
     ⋮



처음과 끝부분 확인할 때는 `first`와 `last` 함수이다.  pandas와 헷갈리는 부분이다. pandas는 `head`와 `tail` 메서드가 대응하는 것들인데, 이름이 같고 기능이 다른 `first`, `last` 메서드가 존재한다.


```julia
first(df, 6)
```




<div class="data-frame"><p>4 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td></tr><tr><th>2</th><td>2</td><td>F</td></tr><tr><th>3</th><td>3</td><td>F</td></tr><tr><th>4</th><td>4</td><td>M</td></tr></tbody></table></div>




```julia
last(df, 6)
```




<div class="data-frame"><p>4 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td></tr><tr><th>2</th><td>2</td><td>F</td></tr><tr><th>3</th><td>3</td><td>F</td></tr><tr><th>4</th><td>4</td><td>M</td></tr></tbody></table></div>



크기가 큰 데이터프레임을 화면에 출력할 때는 아래와 같이 `show` 함수를 사용한다.
```julia
show(df, allrows=true, allcols=true)
```

데이터프레임의 기본적인 통계량과 데이터 타입 등을 조사할 때는 `describe` 함수를 사용한다.


```julia
describe(df)
```




<div class="data-frame"><p>2 rows × 7 columns</p><table class="data-frame"><thead><tr><th></th><th>variable</th><th>mean</th><th>min</th><th>median</th><th>max</th><th>nmissing</th><th>eltype</th></tr><tr><th></th><th title="Symbol">Symbol</th><th title="Union{Nothing, Float64}">Union…</th><th title="Any">Any</th><th title="Union{Nothing, Float64}">Union…</th><th title="Any">Any</th><th title="Int64">Int64</th><th title="DataType">DataType</th></tr></thead><tbody><tr><th>1</th><td>A</td><td>2.5</td><td>1</td><td>2.5</td><td>4</td><td>0</td><td>Int64</td></tr><tr><th>2</th><td>B</td><td></td><td>F</td><td></td><td>M</td><td>0</td><td>String</td></tr></tbody></table></div>



컬럼의 중복 제거된 값들을 조사할 때는 `unique` 함수를 사용한다.


```julia
unique(german.Sex)
```




    2-element Vector{String}:
     ⋮




```julia
[unique(c) for c in eachcol(german)]
```




    10-element Vector{Vector{T} where T}:
     ⋮



컬럼의 데이터 타입을 조사할 때는 `eltype` 함수를 사용한다.


```julia
eltype(german.Sex)
```




    String



# 데이터프레임 행과 열의 추가

빈 DataFrame을 하나 만들고 row를 추가하는 방법도 생각해 볼 수 있다. 빈 데이터프레임은 DataFrame()으로 만들 수 있는데 인자로 컬럼 이름과 데이터 타입만 정의할 수도 있다.


```julia
df = DataFrame(A = Int[], B = String[])
```




<div class="data-frame"><p>0 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody></tbody></table></div>



row를 추가할 때는 tuple이나 vector를 갖다 주면 된다. column과 같은 순서로 요소를 배열해야 한다.  
collection에다가 요소를 추가하는 push!함수를 쓰는 모양이다.


```julia
push!(df, (1, "M"))
push!(df, [2, "N"])
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td></tr><tr><th>2</th><td>2</td><td>N</td></tr></tbody></table></div>



`Dict` 타입으로도 추가할 수 있다.  이거를 사용할 때는 컬럼 이름을 key로 사용한다.


```julia
push!(df, Dict(:B => "F", :A => 3))
```




<div class="data-frame"><p>3 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td></tr><tr><th>2</th><td>2</td><td>N</td></tr><tr><th>3</th><td>3</td><td>F</td></tr></tbody></table></div>



새로운 열을 추가한다. `4:6`은 Julia의 collection 중 하나인 range 개체이다.


```julia
df.C = 4:6
df
```




<div class="data-frame"><p>3 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td><td>4</td></tr><tr><th>2</th><td>2</td><td>N</td><td>5</td></tr><tr><th>3</th><td>3</td><td>F</td><td>6</td></tr></tbody></table></div>



# 필터 Filtering dataframe

값의 변경 여부라는 관점에서 Julia 데이터프레임에 접근하는 방법에는 두 가지가 있다. 원본에 직접 접근하는 방법과 복사본을 만들어서 접근하는 방법이다. 이를 지칭하는 적절한 한국어는 아직 없어서 영어를 그대로 쓰도록 한다.  전자는 referencing, 후자는 copying이라고 부르자. 이러한 개념은 파이썬에도 있다. 웬만한 프로그래밍 언어에는 다 있는 것인가 보다.

또한 데이터프레임에 필터를 걸어 전체 또는 일부를 보는 방법에도 2가지 표현이 있다.
1. `Dataframe.column_selector` : 특정 column에 접근하는 방법.
2. `Dataframe[row_selector, column_selector]` : 특정 row와 column에 접근하는 방법.

이 중 1번은 언제나 referencing 개념으로 접근하게 된다. 2번은 두 가지 방법이 다 가능한데 row_selector에 `!`를 쓰게 되면 referencing, `:`를 쓰게 되면 copying으로 접근하게 된다.

한 개의 column을 선택하는 방법에는 아래와 같이 6가지가 있고 처음 4개는 referecing, 마지막 2개는 copying에 의한 접근이다.


```julia
df.A
```




    3-element Vector{Int64}:
     ⋮




```julia
df."A"
```




    3-element Vector{Int64}:
     ⋮




```julia
df[!, :A]
```




    3-element Vector{Int64}:
     ⋮



`:A`는 symbol이라고 부르는 Julia의 특징이다. 아직 뭔지는 잘 모른다. 아무튼 column 이름에는 symbol과 string을 사용하는 것이 가능하다.


```julia
df[!, "A"]
```




    3-element Vector{Int64}:
     ⋮




```julia
df[:, :A]
```




    3-element Vector{Int64}:
     ⋮




```julia
df[:, "A"]
```




    3-element Vector{Int64}:
     ⋮



6개 모두 vector를 반환한다.  데이터프레임이 필요하면 column을 vector 형태로 전달하면 된다.


```julia
df[!, [:A]]
```




<div class="data-frame"><p>3 rows × 1 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th></tr><tr><th></th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td></tr><tr><th>2</th><td>2</td></tr><tr><th>3</th><td>3</td></tr></tbody></table></div>




```julia
df[:, ["A"]]
```




<div class="data-frame"><p>3 rows × 1 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th></tr><tr><th></th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td></tr><tr><th>2</th><td>2</td></tr><tr><th>3</th><td>3</td></tr></tbody></table></div>



2번 방법의 row와 columns selector에는 위치를 나타내는 정수 인덱스를 사용할 수 있다. Julia는 Python과 달리 1부터 인덱스가 시작한다. 그리고 range 개체를 전달하면 해당하는 row와 column을 뽑을 수 있는데 python과 달리 마지막 인덱스에 사용된 row도 포함된다.


```julia
df[:, 1]
```




    3-element Vector{Int64}:
     ⋮




```julia
df[1:3, :]
```




<div class="data-frame"><p>3 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td><td>4</td></tr><tr><th>2</th><td>2</td><td>N</td><td>5</td></tr><tr><th>3</th><td>3</td><td>F</td><td>6</td></tr></tbody></table></div>




```julia
df[[1, 3], :]
```




<div class="data-frame"><p>2 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td><td>4</td></tr><tr><th>2</th><td>3</td><td>F</td><td>6</td></tr></tbody></table></div>



무조건 1, 2, 3으로 바뀌는 것을 보니 기존의 row index가 유지되는 거 같지는 않다. pandas와는 다르게 `[ ]` operator 하나만 가지고 label과 position 인덱싱이 다 되는 것은 편하다.


```julia
df[:, [:A, :B]]
```




<div class="data-frame"><p>3 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>M</td></tr><tr><th>2</th><td>2</td><td>N</td></tr><tr><th>3</th><td>3</td><td>F</td></tr></tbody></table></div>




```julia
df[1:3, [:B, :A]]
```




<div class="data-frame"><p>3 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>B</th><th>A</th></tr><tr><th></th><th title="String">String</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>M</td><td>1</td></tr><tr><th>2</th><td>N</td><td>2</td></tr><tr><th>3</th><td>F</td><td>3</td></tr></tbody></table></div>




```julia
df[[3, 1], [:C]]
```




<div class="data-frame"><p>2 rows × 1 columns</p><table class="data-frame"><thead><tr><th></th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>6</td></tr><tr><th>2</th><td>4</td></tr></tbody></table></div>



column 이름을 선택할 때는 regular expression도 활용할 수 있다.


```julia
df = DataFrame(x1=1, x2=2, y=3)
df[:, r"x"]
```




<div class="data-frame"><p>1 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>2</td></tr></tbody></table></div>



복잡한 column 선택을 위해서 `Not`, `Between`, `Cols`, `All` 함수를 활용할 수 있다.


```julia
df = DataFrame(r=1, x1=2, x2=3, y=4)
```




<div class="data-frame"><p>1 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>r</th><th>x1</th><th>x2</th><th>y</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>2</td><td>3</td><td>4</td></tr></tbody></table></div>



x가 포함된 이름을 갖는 컬럼들을 맨 앞에 놓는 방법이다.


```julia
df[:, Cols(r"x", :)]
```




<div class="data-frame"><p>1 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th><th>r</th><th>y</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>2</td><td>3</td><td>1</td><td>4</td></tr></tbody></table></div>



x가 포함된 이름을 갖는 컬럼들을 맨 뒤에 놓는 방법이다.


```julia
df[:, Cols(Not(r"x"), :)]
```




<div class="data-frame"><p>1 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>r</th><th>y</th><th>x1</th><th>x2</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>4</td><td>2</td><td>3</td></tr></tbody></table></div>



pandas처럼 row_selctor에 boolean array를 전달하면 해당하는 row를 선택할 수 있다.


```julia
df = DataFrame(A = 1:2:1000, B = repeat(1:10, inner=50), C = 1:500)
```




<div class="data-frame"><p>500 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>1</td><td>1</td></tr><tr><th>2</th><td>3</td><td>1</td><td>2</td></tr><tr><th>3</th><td>5</td><td>1</td><td>3</td></tr><tr><th>4</th><td>7</td><td>1</td><td>4</td></tr><tr><th>5</th><td>9</td><td>1</td><td>5</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table></div>




```julia
df[df.A .> 500, :]
```




<div class="data-frame"><p>250 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>501</td><td>6</td><td>251</td></tr><tr><th>2</th><td>503</td><td>6</td><td>252</td></tr><tr><th>3</th><td>505</td><td>6</td><td>253</td></tr><tr><th>4</th><td>507</td><td>6</td><td>254</td></tr><tr><th>5</th><td>509</td><td>6</td><td>255</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table></div>



Broadcasting을 일으키기 위해서는 연산자 앞에 `.`을 붙여야 한다는 것이 pandas와의 차이점이다.  또한 열을 나타내는 위치의 `:`는 생략할 수 없다.  역시 기존의 row index는 다 무시된다. 아무리 봐도 Julia Dataframe에는 pandas와 같은 index 개념이 없는 듯 하다.  위의 거는 이해하기 어렵지 않은데 아래 거는 복잡하다.


```julia
df[(df.A .> 500) .& (300 .< df.C .< 400), :]
```




<div class="data-frame"><p>99 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>601</td><td>7</td><td>301</td></tr><tr><th>2</th><td>603</td><td>7</td><td>302</td></tr><tr><th>3</th><td>605</td><td>7</td><td>303</td></tr><tr><th>4</th><td>607</td><td>7</td><td>304</td></tr><tr><th>5</th><td>609</td><td>7</td><td>305</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table></div>



`&` 연산자에도 `.`을 해주어야 broadcasting이 된다. 이해하기 어려운 부분이었다.   

아래는 A 컬럼에서 1, 5, 601의 값을 갖는 행들을 추출하는 방법이다. pandas의 `isin` 메서드와 같은 역할을 하는 Julia의 `in` 함수를 사용한다. `Ref` 함수는 broadcasting 과정 중에서 인자로 받는 collection을 scalar로 처리되게 하는 역할을 한다고 한다.  

`in` 다음에도 `.`이 붙어야 하나 보다. 저거 빼고 해보면 에러가 발생한다.


```julia
df[in.(df.A, Ref([1, 5, 601])), :]
```




<div class="data-frame"><p>3 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>1</td><td>1</td></tr><tr><th>2</th><td>5</td><td>1</td><td>3</td></tr><tr><th>3</th><td>601</td><td>7</td><td>301</td></tr></tbody></table></div>



아래와 같이 해도 된다고 하는데 이 때의 `in([1, 5, 10])`은 그 자체로 함수가 된다고 한다. 그러니까 그 다음에 보통 함수에 인자를 전달할 때 사용하는 것처럼 생긴 `(df.A)`의 표현이 올 수 있는 것 같다. 여기서도 그 사이에 `.`을 넣어서 broadcasting을 하고 있다.


```julia
df[in([1, 5, 601]).(df.A), :]
```




<div class="data-frame"><p>3 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>1</td><td>1</td></tr><tr><th>2</th><td>5</td><td>1</td><td>3</td></tr><tr><th>3</th><td>601</td><td>7</td><td>301</td></tr></tbody></table></div>



지금까지 데이터프레임의 부분을 뽑아 낼 때 사용한 표현들은 모두 copying 접근법에 해당한다.

referencing 접근법에 해당하는 상황들을 정리하면 다음과 같다.
- `!`을 사용할 때: `df[!, :A]`, `df[!, [:A, :B]]`
- `.` 표현법: `df.A`
- 한 개의 줄이 정수 표현법에 의해 선택될 때: `df[1, [:A, :B]]`
- `view` 또는 `@view`가 사용되었을 때: `@view df[1:3, :A]

# select와 transform

데이터프레임을 사용하다 보면 column 기반의 작업이 많이 일어난다. column을 다루는 이 2개의 함수에 대해 살펴보자.

`select` 함수는 전달받은 인자를 가지고 데이터프레임의 복사본을 만들어 낸다. 그리고 전달받은 인자에 column이 하나만 있어도 vector가 아니고 데이터프레임을 만든다. 복사본이 아니라 원본의 값을 바꾸려면 `copycols=false`를 전달하면 된다.  아니면 `select!`를 사용한다.


```julia
df = DataFrame(x1=[1, 2], x2=[3, 4], y=[5, 6])
```




<div class="data-frame"><p>2 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th><th>y</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td><td>5</td></tr><tr><th>2</th><td>2</td><td>4</td><td>6</td></tr></tbody></table></div>



x1 column 삭제하기.


```julia
select(df, Not(:x1))
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x2</th><th>y</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>3</td><td>5</td></tr><tr><th>2</th><td>4</td><td>6</td></tr></tbody></table></div>



힘은 들지만 이렇게 해도 된다.


```julia
select(df, [:x1, :y])
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>y</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>5</td></tr><tr><th>2</th><td>2</td><td>6</td></tr></tbody></table></div>



이름에 'x'가 있는 column 선택하기. Julia의 regular expression은 보통 r"..."의 형태로 적는다.


```julia
select(df, r"x")
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td></tr><tr><th>2</th><td>2</td><td>4</td></tr></tbody></table></div>



column 이름 바꾸기. =>는 Pair를 만들어내는 operator이다.


```julia
select(df, :x1 => :a1, :x2 => :a2)
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>a1</th><th>a2</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td></tr><tr><th>2</th><td>2</td><td>4</td></tr></tbody></table></div>



column 단위로 함수를 적용하기. x -> x .- minimum(x)는 python의 람다 함수같은 거다. 익명함수 anonymous function 이라고 부른다. 여기에도 `.-`와 같이 broadcasting이 들어 있다. `.` 빼먹으면 error 발생한다.  

여기에서 =>는 2개가 연결되어 있는 형태로 사용되었는데 이것도 Pair라고 부를까? 아니면 그냥 select 함수의 문법일까?


```julia
select(df, :x1, :x2 => (x -> x .- minimum(x)) => :x2)
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>0</td></tr><tr><th>2</th><td>2</td><td>1</td></tr></tbody></table></div>




```julia
select(df, :x1, :x2 => (x -> x .- minimum(x)))
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2_function</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>0</td></tr><tr><th>2</th><td>2</td><td>1</td></tr></tbody></table></div>




```julia
select(df, :x1, :x2 => (x -> x .- minimum(x)) => :x3)
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x3</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>0</td></tr><tr><th>2</th><td>2</td><td>1</td></tr></tbody></table></div>



Broadcasting의 또 다른 방법 `ByRow`. 결과적으로 생성되는 column 이름을 기억해 둘 필요가 있다.


```julia
select(df, :x2, :x2 => ByRow(sqrt))
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x2</th><th>x2_sqrt</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>3</td><td>1.73205</td></tr><tr><th>2</th><td>4</td><td>2.0</td></tr></tbody></table></div>




```julia
select(df, :x2, :x2 => (x -> sqrt.(x)) )
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x2</th><th>x2_function</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>3</td><td>1.73205</td></tr><tr><th>2</th><td>4</td><td>2.0</td></tr></tbody></table></div>




```julia
select(df, :x2, :x2 => ByRow(sqrt) => :x3)
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x2</th><th>x3</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>3</td><td>1.73205</td></tr><tr><th>2</th><td>4</td><td>2.0</td></tr></tbody></table></div>



여러 개의 column을 한꺼번에 다루기. `extrema`는 iterator를 인자로 받아 minimum과 maximum을 tuple로 반환하는 함수이다.


```julia
select(df, AsTable(:) => ByRow(extrema))
```




<div class="data-frame"><p>2 rows × 1 columns</p><table class="data-frame"><thead><tr><th></th><th>x1_x2_y_extrema</th></tr><tr><th></th><th title="Tuple{Int64, Int64}">Tuple…</th></tr></thead><tbody><tr><th>1</th><td>(1, 5)</td></tr><tr><th>2</th><td>(2, 6)</td></tr></tbody></table></div>




```julia
select(df, AsTable(:) => ByRow(extrema) => [:lo, :hi])
```




<div class="data-frame"><p>2 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>lo</th><th>hi</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>5</td></tr><tr><th>2</th><td>2</td><td>6</td></tr></tbody></table></div>




```julia
select(df, AsTable([:x1, :x2]) => ByRow(extrema))
```




<div class="data-frame"><p>2 rows × 1 columns</p><table class="data-frame"><thead><tr><th></th><th>x1_x2_extrema</th></tr><tr><th></th><th title="Tuple{Int64, Int64}">Tuple…</th></tr></thead><tbody><tr><th>1</th><td>(1, 3)</td></tr><tr><th>2</th><td>(2, 4)</td></tr></tbody></table></div>




```julia
df
```




<div class="data-frame"><p>2 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th><th>y</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td><td>5</td></tr><tr><th>2</th><td>2</td><td>4</td><td>6</td></tr></tbody></table></div>



`transform`은 `select`와 같은데, 입력되는 데이터프레임의 모든 column을 포함한다는 점만 다르다.

`All()` selector를 사용하여 행방향 합계를 구하는 표현을 예로 들어 보자.


```julia
df = DataFrame(x1=[1, 2], x2=[3, 4], y=[5, 6])
```




<div class="data-frame"><p>2 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th><th>y</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td><td>5</td></tr><tr><th>2</th><td>2</td><td>4</td><td>6</td></tr></tbody></table></div>




```julia
transform(df, All() => +)
```




<div class="data-frame"><p>2 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th><th>y</th><th>x1_x2_y_+</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td><td>5</td><td>9</td></tr><tr><th>2</th><td>2</td><td>4</td><td>6</td><td>12</td></tr></tbody></table></div>




```julia
using Statistics
```


```julia
transform(df, AsTable(:) => ByRow(sum))
```




<div class="data-frame"><p>2 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th><th>y</th><th>x1_x2_y_sum</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td><td>5</td><td>9</td></tr><tr><th>2</th><td>2</td><td>4</td><td>6</td><td>12</td></tr></tbody></table></div>




```julia
transform(df, AsTable(:) => sum)
```




<div class="data-frame"><p>2 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>x1</th><th>x2</th><th>y</th><th>x1_x2_y_sum</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Int64">Int64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>3</td><td>5</td><td>9</td></tr><tr><th>2</th><td>2</td><td>4</td><td>6</td><td>12</td></tr></tbody></table></div>



`ByRow` wrapper를 사용하여 각 행에서 최대값을 갖는 열 이름을 찾아낼 수 있다.


```julia
using Random
```


```julia
df = DataFrame(rand(10, 3), [:a, :b, :c])
```




<div class="data-frame"><p>10 rows × 3 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th></tr><tr><th></th><th title="Float64">Float64</th><th title="Float64">Float64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>0.124854</td><td>0.098039</td><td>0.284497</td></tr><tr><th>2</th><td>0.85271</td><td>0.216097</td><td>0.52116</td></tr><tr><th>3</th><td>0.0279124</td><td>0.693856</td><td>0.210384</td></tr><tr><th>4</th><td>0.800491</td><td>0.43282</td><td>0.266901</td></tr><tr><th>5</th><td>0.387098</td><td>0.129767</td><td>0.94161</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table></div>




```julia
transform(df, AsTable(:) => ByRow(argmax) => :prediction)
```




<div class="data-frame"><p>10 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>prediction</th></tr><tr><th></th><th title="Float64">Float64</th><th title="Float64">Float64</th><th title="Float64">Float64</th><th title="Symbol">Symbol</th></tr></thead><tbody><tr><th>1</th><td>0.124854</td><td>0.098039</td><td>0.284497</td><td>c</td></tr><tr><th>2</th><td>0.85271</td><td>0.216097</td><td>0.52116</td><td>a</td></tr><tr><th>3</th><td>0.0279124</td><td>0.693856</td><td>0.210384</td><td>b</td></tr><tr><th>4</th><td>0.800491</td><td>0.43282</td><td>0.266901</td><td>a</td></tr><tr><th>5</th><td>0.387098</td><td>0.129767</td><td>0.94161</td><td>c</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table></div>




```julia
df = DataFrame(x=[1, 2, missing], y=[1, missing, missing])
```




<div class="data-frame"><p>3 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>x</th><th>y</th></tr><tr><th></th><th title="Union{Missing, Int64}">Int64?</th><th title="Union{Missing, Int64}">Int64?</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>1</td></tr><tr><th>2</th><td>2</td><td><em>missing</em></td></tr><tr><th>3</th><td><em>missing</em></td><td><em>missing</em></td></tr></tbody></table></div>



`∘`: 함수를 연결한다. 즉, `(f ∘ g)(args...)`는 `f(g(args...))`와 같다.  
`skipmissing`: 인자로 전달받은 iterator 중에 missing값이 있으면 그것을 건너 띈 iterator를 돌려주는 함수.  
`count([f=identity,] itr; init=0) -> Integer`: itr 중에 f의 결과가 true인 요소의 갯수를 반환하는 함수.  


```julia
transform(df, AsTable(:) .=>
              ByRow.([sum∘skipmissing,
                      x -> count(!ismissing, x),
                      mean∘skipmissing]) .=>
              [:sum, :n, :mean])
```




<div class="data-frame"><p>3 rows × 5 columns</p><table class="data-frame"><thead><tr><th></th><th>x</th><th>y</th><th>sum</th><th>n</th><th>mean</th></tr><tr><th></th><th title="Union{Missing, Int64}">Int64?</th><th title="Union{Missing, Int64}">Int64?</th><th title="Int64">Int64</th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>1</td><td>2</td><td>2</td><td>1.0</td></tr><tr><th>2</th><td>2</td><td><em>missing</em></td><td>2</td><td>1</td><td>2.0</td></tr><tr><th>3</th><td><em>missing</em></td><td><em>missing</em></td><td>0</td><td>0</td><td>NaN</td></tr></tbody></table></div>



# Combine

함수에 column을 인자로 전달해주고 결과를 column에 맞추어 배열하는 dataframe을 반환한다.


```julia
df = DataFrame(A = 1:4, B = 4.0:-1.0:1.0)
```




<div class="data-frame"><p>4 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>4.0</td></tr><tr><th>2</th><td>2</td><td>3.0</td></tr><tr><th>3</th><td>3</td><td>2.0</td></tr><tr><th>4</th><td>4</td><td>1.0</td></tr></tbody></table></div>




```julia
combine(df, names(df) .=> sum)
```




<div class="data-frame"><p>1 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A_sum</th><th>B_sum</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>10</td><td>10.0</td></tr></tbody></table></div>




```julia
combine(df, propertynames(df) .=> sum)
```




<div class="data-frame"><p>1 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A_sum</th><th>B_sum</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>10</td><td>10.0</td></tr></tbody></table></div>




```julia
combine(df, :A => sum, :B => sum)
```




<div class="data-frame"><p>1 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>A_sum</th><th>B_sum</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>10</td><td>10.0</td></tr></tbody></table></div>




```julia
combine(df, names(df) .=> sum, names(df) .=> prod)
```




<div class="data-frame"><p>1 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>A_sum</th><th>B_sum</th><th>A_prod</th><th>B_prod</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr></tbody></table></div>



row의 수를 유지하려면 `select`를 쓰고 원래의 column을 유지하려면 `transform`을 쓸 것.


```julia
select(df, names(df) .=> sum, names(df) .=> prod)
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>A_sum</th><th>B_sum</th><th>A_prod</th><th>B_prod</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr><tr><th>2</th><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr><tr><th>3</th><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr><tr><th>4</th><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr></tbody></table></div>




```julia
transform(df, names(df) .=> sum, names(df) .=> prod)
```




<div class="data-frame"><p>4 rows × 6 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>A_sum</th><th>B_sum</th><th>A_prod</th><th>B_prod</th></tr><tr><th></th><th title="Int64">Int64</th><th title="Float64">Float64</th><th title="Int64">Int64</th><th title="Float64">Float64</th><th title="Int64">Int64</th><th title="Float64">Float64</th></tr></thead><tbody><tr><th>1</th><td>1</td><td>4.0</td><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr><tr><th>2</th><td>2</td><td>3.0</td><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr><tr><th>3</th><td>3</td><td>2.0</td><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr><tr><th>4</th><td>4</td><td>1.0</td><td>10</td><td>10.0</td><td>24</td><td>24.0</td></tr></tbody></table></div>



# Dataframe 값의 변경  Replacing value in dataframe

하나의 column에 대해 값을 변경하는 기능은 `replace!` 함수를 사용하면 된다.


```julia
df = DataFrame(a = ["a", "None", "b", "None"],
               b = 1:4,
               c = ["None", "j", "k", "h"],
               d = ["x", "y", "None", "z"])
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="String">String</th><th title="Int64">Int64</th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1</td><td>None</td><td>x</td></tr><tr><th>2</th><td>None</td><td>2</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3</td><td>k</td><td>None</td></tr><tr><th>4</th><td>None</td><td>4</td><td>h</td><td>z</td></tr></tbody></table></div>




```julia
replace!(df.a, "None" => "c")
```




    4-element Vector{String}:
     ⋮




```julia
df
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="String">String</th><th title="Int64">Int64</th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1</td><td>None</td><td>x</td></tr><tr><th>2</th><td>c</td><td>2</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3</td><td>k</td><td>None</td></tr><tr><th>4</th><td>c</td><td>4</td><td>h</td><td>z</td></tr></tbody></table></div>



여러 column이나 dataframe 전체에 대한 변경은 broadcasting 문법을 사용한다.


```julia
# replacement on a subset of columns [:c, :d]
df[:, [:c, :d]] .= ifelse.(df[!, [:c, :d]] .== "None", "c", df[!, [:c, :d]])
```




<div class="data-frame"><p>4 rows × 2 columns</p><table class="data-frame"><thead><tr><th></th><th>c</th><th>d</th></tr><tr><th></th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>c</td><td>x</td></tr><tr><th>2</th><td>j</td><td>y</td></tr><tr><th>3</th><td>k</td><td>c</td></tr><tr><th>4</th><td>h</td><td>z</td></tr></tbody></table></div>



`ifelse(condition::Bool, x, y)`: condition이 true이면 x, false이면 y를 반환하는 함수.


```julia
# replacement on entire data frame
df .= ifelse.(df .== "c", "None", df)
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="String">String</th><th title="Int64">Int64</th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1</td><td>None</td><td>x</td></tr><tr><th>2</th><td>None</td><td>2</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3</td><td>k</td><td>None</td></tr><tr><th>4</th><td>None</td><td>4</td><td>h</td><td>z</td></tr></tbody></table></div>




```julia
df
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="String">String</th><th title="Int64">Int64</th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1</td><td>None</td><td>x</td></tr><tr><th>2</th><td>None</td><td>2</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3</td><td>k</td><td>None</td></tr><tr><th>4</th><td>None</td><td>4</td><td>h</td><td>z</td></tr></tbody></table></div>



> **Missing, nothing, NaN**  
> Julia는 결측값을 나타내는 데이터 타입을 갖추고 있다.  
> - `nothing` (type `Nothing`): code block이나 함수로부터 아무 것도 돌려줄 것이 없다는 의미의 값.
> - `missing` (type `Missing`): 통계학에서 말하는 잃어버린 값. 값이 있어야 하지만 알수 없다는 뜻임.  
> - `NaN` (type `Float64`): 숫자가 아닌 값을 나타냄.

missing 값으로 변경하고자 할 때는, 그 column이 missing을 받아들일 수 있는 data type이 아니면 in-place 변경은 하지 말고 copy 개념으로 작업이 되도록 하는 것이 좋다. 원본을 변경하려면 미리 allowmissing!을 선언해두어야 한다.


```julia
# do not operate in-place (`df = ` would also work)
df2 = ifelse.(df .== "None", missing, df) 
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="Union{Missing, String}">String?</th><th title="Int64">Int64</th><th title="Union{Missing, String}">String?</th><th title="Union{Missing, String}">String?</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1</td><td><em>missing</em></td><td>x</td></tr><tr><th>2</th><td><em>missing</em></td><td>2</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3</td><td>k</td><td><em>missing</em></td></tr><tr><th>4</th><td><em>missing</em></td><td>4</td><td>h</td><td>z</td></tr></tbody></table></div>




```julia
allowmissing!(df)
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="Union{Missing, String}">String?</th><th title="Union{Missing, Int64}">Int64?</th><th title="Union{Missing, String}">String?</th><th title="Union{Missing, String}">String?</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1</td><td>None</td><td>x</td></tr><tr><th>2</th><td>None</td><td>2</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3</td><td>k</td><td>None</td></tr><tr><th>4</th><td>None</td><td>4</td><td>h</td><td>z</td></tr></tbody></table></div>




```julia
df .= ifelse.(df .== "None", missing, df) 
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="Union{Missing, String}">String?</th><th title="Union{Missing, Int64}">Int64?</th><th title="Union{Missing, String}">String?</th><th title="Union{Missing, String}">String?</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1</td><td><em>missing</em></td><td>x</td></tr><tr><th>2</th><td><em>missing</em></td><td>2</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3</td><td>k</td><td><em>missing</em></td></tr><tr><th>4</th><td><em>missing</em></td><td>4</td><td>h</td><td>z</td></tr></tbody></table></div>



## Header(=column 이름) 바꾸기 


```julia
df = DataFrame(a = ["a", "None", "b", "None"],
               b = ["1,000", "2,000", "3,000", "4,000"],
               c = ["None", "j", "k", "h"],
               d = ["x", "y", "None", "z"])
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th title="String">String</th><th title="String">String</th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1,000</td><td>None</td><td>x</td></tr><tr><th>2</th><td>None</td><td>2,000</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3,000</td><td>k</td><td>None</td></tr><tr><th>4</th><td>None</td><td>4,000</td><td>h</td><td>z</td></tr></tbody></table></div>




```julia
rename!(df, [:A, :B, :C, :D])
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th><th>D</th></tr><tr><th></th><th title="String">String</th><th title="String">String</th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1,000</td><td>None</td><td>x</td></tr><tr><th>2</th><td>None</td><td>2,000</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3,000</td><td>k</td><td>None</td></tr><tr><th>4</th><td>None</td><td>4,000</td><td>h</td><td>z</td></tr></tbody></table></div>



## Column의 data type 바꾸기


```julia
# 먼저 ,를 제거
df.B = replace.(df.B, "," => "")
df.B = parse.(Int, df.B)
df
```




<div class="data-frame"><p>4 rows × 4 columns</p><table class="data-frame"><thead><tr><th></th><th>A</th><th>B</th><th>C</th><th>D</th></tr><tr><th></th><th title="String">String</th><th title="Int64">Int64</th><th title="String">String</th><th title="String">String</th></tr></thead><tbody><tr><th>1</th><td>a</td><td>1000</td><td>None</td><td>x</td></tr><tr><th>2</th><td>None</td><td>2000</td><td>j</td><td>y</td></tr><tr><th>3</th><td>b</td><td>3000</td><td>k</td><td>None</td></tr><tr><th>4</th><td>None</td><td>4000</td><td>h</td><td>z</td></tr></tbody></table></div>



# Join
- `innerjoin`: the output contains rows for values of the key that exist in all passed data frames.
- `leftjoin`: the output contains rows for values of the key that exist in the first (left) argument, whether or not that value exists in the second (right) argument.
- `rightjoin`: the output contains rows for values of the key that exist in the second (right) argument, whether or not that value exists in the first (left) argument.
- `outerjoin`: the output contains rows for values of the key that exist in any of the passed data frames.
- `semijoin`: Like an inner join, but output is restricted to columns from the first (left) argument.
- `antijoin`: The output contains rows for values of the key that exist in the first (left) but not the second (right) argument. As with semijoin, output is restricted to columns from the first (left) argument.
- `crossjoin`: The output is the cartesian product of rows from all passed data frames.

`semijoin`, `antijoin` 함수는 쓸 일이 있을 지 잘 모르겠다. 사용하는 형태는 `crossjoin`을 뺀 모든 join 함수가 아래와 같다. key가 되는 column을 `on` 키워드 다음에 써주면 된다.


```julia
people = DataFrame(ID = [20, 40], Name = ["John Doe", "Jane Doe"])
```




<table class="data-frame"><thead><tr><th></th><th>ID</th><th>Name</th></tr><tr><th></th><th>Int64</th><th>String</th></tr></thead><tbody><p>2 rows × 2 columns</p><tr><th>1</th><td>20</td><td>John Doe</td></tr><tr><th>2</th><td>40</td><td>Jane Doe</td></tr></tbody></table>




```julia
jobs = DataFrame(ID = [20, 40], Job = ["Lawyer", "Doctor"])
```




<table class="data-frame"><thead><tr><th></th><th>ID</th><th>Job</th></tr><tr><th></th><th>Int64</th><th>String</th></tr></thead><tbody><p>2 rows × 2 columns</p><tr><th>1</th><td>20</td><td>Lawyer</td></tr><tr><th>2</th><td>40</td><td>Doctor</td></tr></tbody></table>




```julia
innerjoin(people, jobs, on = :ID)
```




<table class="data-frame"><thead><tr><th></th><th>ID</th><th>Name</th><th>Job</th></tr><tr><th></th><th>Int64</th><th>String</th><th>String</th></tr></thead><tbody><p>2 rows × 3 columns</p><tr><th>1</th><td>20</td><td>John Doe</td><td>Lawyer</td></tr><tr><th>2</th><td>40</td><td>Jane Doe</td><td>Doctor</td></tr></tbody></table>



`crossjoin`은 key가 필요없다고 한다. `makeunique` 키워드에 false를 넣어 봤더니 error가 발생했다. 웬만하면 같이 써 줄 필요가 있는 거 같다.


```julia
crossjoin(people, jobs, makeunique = true)
```




<table class="data-frame"><thead><tr><th></th><th>ID</th><th>Name</th><th>ID_1</th><th>Job</th></tr><tr><th></th><th>Int64</th><th>String</th><th>Int64</th><th>String</th></tr></thead><tbody><p>4 rows × 4 columns</p><tr><th>1</th><td>20</td><td>John Doe</td><td>20</td><td>Lawyer</td></tr><tr><th>2</th><td>20</td><td>John Doe</td><td>40</td><td>Doctor</td></tr><tr><th>3</th><td>40</td><td>Jane Doe</td><td>20</td><td>Lawyer</td></tr><tr><th>4</th><td>40</td><td>Jane Doe</td><td>40</td><td>Doctor</td></tr></tbody></table>



좀 복잡한 예를 하나 들면 다 설명이 될 것 같다. key가 여러 개의 column이고 서로의 이름도 다를 경우이다.  
City와 Location, Job과 Work가 각각 같은 내용을 갖는 다른 이름의 key 컬럼들이며 아래와 같이 pair의 vector로 표시한다.


```julia
a = DataFrame(City = ["Amsterdam", "London", "London", "New York", "New York"],
              Job = ["Lawyer", "Lawyer", "Lawyer", "Doctor", "Doctor"],
              Category = [1, 2, 3, 4, 5])
```




<table class="data-frame"><thead><tr><th></th><th>City</th><th>Job</th><th>Category</th></tr><tr><th></th><th>String</th><th>String</th><th>Int64</th></tr></thead><tbody><p>5 rows × 3 columns</p><tr><th>1</th><td>Amsterdam</td><td>Lawyer</td><td>1</td></tr><tr><th>2</th><td>London</td><td>Lawyer</td><td>2</td></tr><tr><th>3</th><td>London</td><td>Lawyer</td><td>3</td></tr><tr><th>4</th><td>New York</td><td>Doctor</td><td>4</td></tr><tr><th>5</th><td>New York</td><td>Doctor</td><td>5</td></tr></tbody></table>




```julia
b = DataFrame(Location = ["Amsterdam", "London", "London", "New York", "New York"],
              Work = ["Lawyer", "Lawyer", "Lawyer", "Doctor", "Doctor"],
              Name = ["a", "b", "c", "d", "e"])
```




<table class="data-frame"><thead><tr><th></th><th>Location</th><th>Work</th><th>Name</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th></tr></thead><tbody><p>5 rows × 3 columns</p><tr><th>1</th><td>Amsterdam</td><td>Lawyer</td><td>a</td></tr><tr><th>2</th><td>London</td><td>Lawyer</td><td>b</td></tr><tr><th>3</th><td>London</td><td>Lawyer</td><td>c</td></tr><tr><th>4</th><td>New York</td><td>Doctor</td><td>d</td></tr><tr><th>5</th><td>New York</td><td>Doctor</td><td>e</td></tr></tbody></table>




```julia
innerjoin(a, b, on = [:City => :Location, :Job => :Work])
```




<table class="data-frame"><thead><tr><th></th><th>City</th><th>Job</th><th>Category</th><th>Name</th></tr><tr><th></th><th>String</th><th>String</th><th>Int64</th><th>String</th></tr></thead><tbody><p>9 rows × 4 columns</p><tr><th>1</th><td>Amsterdam</td><td>Lawyer</td><td>1</td><td>a</td></tr><tr><th>2</th><td>London</td><td>Lawyer</td><td>2</td><td>b</td></tr><tr><th>3</th><td>London</td><td>Lawyer</td><td>2</td><td>c</td></tr><tr><th>4</th><td>London</td><td>Lawyer</td><td>3</td><td>b</td></tr><tr><th>5</th><td>London</td><td>Lawyer</td><td>3</td><td>c</td></tr><tr><th>6</th><td>New York</td><td>Doctor</td><td>4</td><td>d</td></tr><tr><th>7</th><td>New York</td><td>Doctor</td><td>4</td><td>e</td></tr><tr><th>8</th><td>New York</td><td>Doctor</td><td>5</td><td>d</td></tr><tr><th>9</th><td>New York</td><td>Doctor</td><td>5</td><td>e</td></tr></tbody></table>



London과 Lawyer처럼 key가 중복되면 2번부터 5번 행과 같이 모든 경우의 수를 다 나타낸다.

# Split-Apply-Combine

데이터 처리 작업에 있어서 다음의 작업을 순차적으로 진행하는 경우가 많이 있다.
1. 데이터를 몇 개의 group으로 나누기  splitting a data set into groups
2. 각 group에 함수를 적용하기  applying some functions to each of the groups
3. 결과를 종합하기  combining the results

1번의 기능은 `groupby` 함수를 통해 수행할 수 있으며 `GroupedDataFrame`을 만들어낸다. 이거에다가 `combine`, `select`, `transform` 함수를 적용할 수 있다.

`GroupedDataFrame`의 상대적 개념은 `DataFrame`이 될 것이다. 이는 하나의 group으로 이루어진  dataframe이라고 이해하면 될 것 같다.

`groupby` 함수에 두 개의 인자를 전달하면 `GroupedDataFrame`이 반환된다. 두 개의 인자는 다음과 같다.
(1) Group으로 나누어질 원래의 데이터프레임  
(2) Group으로 나누는 기준이 되는 값을 갖는 column의 집합


```julia
using CSV, Statistics
```


```julia
iris = DataFrame(CSV.File("iris.csv"))
```




<table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th></tr></thead><tbody><p>150 rows × 5 columns</p><tr><th>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td><td>Iris-setosa</td></tr><tr><th>7</th><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td><td>Iris-setosa</td></tr><tr><th>8</th><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>9</th><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>10</th><td>4.9</td><td>3.1</td><td>1.5</td><td>0.1</td><td>Iris-setosa</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>




```julia
gdf = groupby(iris, :Species)
```




<p><b>GroupedDataFrame with 3 groups based on key: Species</b></p><p><i>First Group (50 rows): Species = "Iris-setosa"</i></p><table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th></tr></thead><tbody><tr><th>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td><td>Iris-setosa</td></tr><tr><th>7</th><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td><td>Iris-setosa</td></tr><tr><th>8</th><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>9</th><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>10</th><td>4.9</td><td>3.1</td><td>1.5</td><td>0.1</td><td>Iris-setosa</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table><p>&vellip;</p><p><i>Last Group (50 rows): Species = "Iris-virginica"</i></p><table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th></tr></thead><tbody><tr><th>1</th><td>6.3</td><td>3.3</td><td>6.0</td><td>2.5</td><td>Iris-virginica</td></tr><tr><th>2</th><td>5.8</td><td>2.7</td><td>5.1</td><td>1.9</td><td>Iris-virginica</td></tr><tr><th>3</th><td>7.1</td><td>3.0</td><td>5.9</td><td>2.1</td><td>Iris-virginica</td></tr><tr><th>4</th><td>6.3</td><td>2.9</td><td>5.6</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>5</th><td>6.5</td><td>3.0</td><td>5.8</td><td>2.2</td><td>Iris-virginica</td></tr><tr><th>6</th><td>7.6</td><td>3.0</td><td>6.6</td><td>2.1</td><td>Iris-virginica</td></tr><tr><th>7</th><td>4.9</td><td>2.5</td><td>4.5</td><td>1.7</td><td>Iris-virginica</td></tr><tr><th>8</th><td>7.3</td><td>2.9</td><td>6.3</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>9</th><td>6.7</td><td>2.5</td><td>5.8</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>10</th><td>7.2</td><td>3.6</td><td>6.1</td><td>2.5</td><td>Iris-virginica</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>



`GroupedDataFrame`의 각 group에 `combine`, `select`, `transform` 함수를 적용한다.


```julia
combine(gdf, :PetalLength => mean)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>PetalLength_mean</th></tr><tr><th></th><th>String</th><th>Float64</th></tr></thead><tbody><p>3 rows × 2 columns</p><tr><th>1</th><td>Iris-setosa</td><td>1.464</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>4.26</td></tr><tr><th>3</th><td>Iris-virginica</td><td>5.552</td></tr></tbody></table>



각 함수에 적용할 수 있는 인자는 다음과 같다.

1. column selector(정수, `Symbol`, 문자열, 얘네들의 vector, `All`, `Cols`, `:`, `Between`, `Not`, regular expression)
2. `cols => function` pair. 이 경우 결과적으로 생성되는 column 이름은 원래의 컬럼에 적용된 함수 이름을 더해서 결정된다. 위의 예에 적용된 경우이다.
3. `cols => function => target_cols` 형태. 결과적으로 생성되는 column 이름을 명시하는 경우이다.
4. `col => target_cols` pair. column 이름이 변경된다.
5. `nrow` 또는 `nrow => target_cols` 형태. group의 row의 수를 계산. target_cols가 주어지지 않은 경우 :nrow 컬럼이 생성됨.
6. 위의 2에서 5번에 해당하는 문법으로 만들어진 pair들의 vector 또는 matrix
7. 각 group을 `SubDataFram`이라고 하는데 이에 대해 적용되는 함수

2번 `cols => function` pair가 인자로 사용된 경우


```julia
combine(gdf, :PetalLength => mean)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>PetalLength_mean</th></tr><tr><th></th><th>String</th><th>Float64</th></tr></thead><tbody><p>3 rows × 2 columns</p><tr><th>1</th><td>Iris-setosa</td><td>1.464</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>4.26</td></tr><tr><th>3</th><td>Iris-virginica</td><td>5.552</td></tr></tbody></table>



5번 `nrow`, 3번 `cols => function => target_cols`을 2, 3번째 인자로 사용한 경우.


```julia
combine(gdf, nrow, :PetalLength => mean => :mean)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>nrow</th><th>mean</th></tr><tr><th></th><th>String</th><th>Int64</th><th>Float64</th></tr></thead><tbody><p>3 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>50</td><td>1.464</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>50</td><td>4.26</td></tr><tr><th>3</th><td>Iris-virginica</td><td>50</td><td>5.552</td></tr></tbody></table>



아래는 여러 개의 column이 인자로 전달되는 3번의 경우라고 생각된다.  
여기 사용된 AsTable에 대해서 Julia 공식 문서는 이렇게 설명하고 있다. 뭔 말인지 아직 모르겠다.

>```AsTable(cols)```
>
>A type used for selection operations to signal that the columns selected by the wrapped selector should be passed as a NamedTuple to the function.
>
>선택하는 절차에 사용되는 type이며, 인자로 전달된 column들이 함수에 NamedTuple로서 전달되어야 함을 의미한다.


```julia
combine(gdf,
        [:PetalLength, :SepalLength] =>
        ((p, s) -> (a=mean(p)/mean(s), b=sum(p))) =>
        AsTable
)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>a</th><th>b</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Float64</th></tr></thead><tbody><p>3 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>0.292449</td><td>73.2</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>0.717655</td><td>213.0</td></tr><tr><th>3</th><td>Iris-virginica</td><td>0.842744</td><td>277.6</td></tr></tbody></table>



AsTable 대신 `[:a, :b]`를 써도 작동함.


```julia
combine(gdf,
        [:PetalLength, :SepalLength] =>
        ((p, s) -> (a=mean(p)/mean(s), b=sum(p))) =>
        [:a, :b]
)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>a</th><th>b</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Float64</th></tr></thead><tbody><p>3 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>0.292449</td><td>73.2</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>0.717655</td><td>213.0</td></tr><tr><th>3</th><td>Iris-virginica</td><td>0.842744</td><td>277.6</td></tr></tbody></table>



NamedTuple을 인자로 전달하는 경우.


```julia
combine(gdf,
        AsTable([:PetalLength, :SepalLength]) =>
        x -> std(x.PetalLength) / std(x.SepalLength)
)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>PetalLength_SepalLength_function</th></tr><tr><th></th><th>String</th><th>Float64</th></tr></thead><tbody><p>3 rows × 2 columns</p><tr><th>1</th><td>Iris-setosa</td><td>0.492245</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>0.910378</td></tr><tr><th>3</th><td>Iris-virginica</td><td>0.867923</td></tr></tbody></table>



`SubDataFrame`을 인자로 전달하는 경우. 2번째 인자인 gdf의 `SubDataFrame`들이 1번째 인자인 익명 함수에 전달되므로 x는 DataFrame 형태가 될 것이다.


```julia
combine(x -> std(x.PetalLength) / std(x.SepalLength), gdf)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>x1</th></tr><tr><th></th><th>String</th><th>Float64</th></tr></thead><tbody><p>3 rows × 2 columns</p><tr><th>1</th><td>Iris-setosa</td><td>0.492245</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>0.910378</td></tr><tr><th>3</th><td>Iris-virginica</td><td>0.867923</td></tr></tbody></table>



이 경우는 `do` block 형태를 이용하여 표현할 수 있다. do ~ end 사이의 내용이 익명 함수로 정의되고 combine의 첫번째 인자로 사용된다.


```julia
combine(gdf) do x
    std(x.PetalLength) / std(x.SepalLength)
end
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>x1</th></tr><tr><th></th><th>String</th><th>Float64</th></tr></thead><tbody><p>3 rows × 2 columns</p><tr><th>1</th><td>Iris-setosa</td><td>0.492245</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>0.910378</td></tr><tr><th>3</th><td>Iris-virginica</td><td>0.867923</td></tr></tbody></table>



데이터프레임을 인자로 받고 두 개의 결과를 return하는 익명함수도 사용할 수 있다.


```julia
combine(gdf) do df
    (m = mean(df.PetalLength), s² = var(df.PetalLength))
end
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>m</th><th>s²</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Float64</th></tr></thead><tbody><p>3 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>1.464</td><td>0.0301061</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>4.26</td><td>0.220816</td></tr><tr><th>3</th><td>Iris-virginica</td><td>5.552</td><td>0.304588</td></tr></tbody></table>



2번 `cols => function`과 5번 `nrow`가 전달된 case. `cor`은 인자로 전달받은 2개의 vector 사이의 Pearson 상관계수를 반환한다.


```julia
combine(gdf, 1:2 => cor, nrow)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>SepalLength_SepalWidth_cor</th><th>nrow</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Int64</th></tr></thead><tbody><p>3 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>0.74678</td><td>50</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>0.525911</td><td>50</td></tr><tr><th>3</th><td>Iris-virginica</td><td>0.457228</td><td>50</td></tr></tbody></table>



3번 `cols => function => target_cols`가 적용된 경우


```julia
combine(gdf,
        :PetalLength => 
        (x -> [extrema(x)]) =>
        [:min, :max])
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>min</th><th>max</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Float64</th></tr></thead><tbody><p>3 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>1.0</td><td>1.9</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>3.0</td><td>5.1</td></tr><tr><th>3</th><td>Iris-virginica</td><td>4.5</td><td>6.9</td></tr></tbody></table>



`(x -> [extrema(x)])`에서 `extrema(x)`를 둘러싸고 있는 `[ ]`를 빼면 error가 발생한다.


```julia
combine(gdf,
        :PetalLength => 
        (x -> [extrema(x)])
)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>PetalLength_function</th></tr><tr><th></th><th>String</th><th>Tuple…</th></tr></thead><tbody><p>3 rows × 2 columns</p><tr><th>1</th><td>Iris-setosa</td><td>(1.0, 1.9)</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>(3.0, 5.1)</td></tr><tr><th>3</th><td>Iris-virginica</td><td>(4.5, 6.9)</td></tr></tbody></table>




```julia
combine(gdf,
        :PetalLength => 
        (x -> extrema(x))
)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>PetalLength_function</th></tr><tr><th></th><th>String</th><th>Tuple…</th></tr></thead><tbody><p>3 rows × 2 columns</p><tr><th>1</th><td>Iris-setosa</td><td>(1.0, 1.9)</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>(3.0, 5.1)</td></tr><tr><th>3</th><td>Iris-virginica</td><td>(4.5, 6.9)</td></tr></tbody></table>



# `GroupdDataFrame`의 본질<br>Structure of `GroupdDataFrame`

collection의 index와 값을 iterator 형태의 값으로 반환해 주는 `pairs` 함수에 `GroupedDataFrame`을 넣어보자.


```julia
pairs(gdf)
```




    Base.Generator{Base.Iterators.Zip{Tuple{DataFrames.GroupKeys{GroupedDataFrame{DataFrame}}, GroupedDataFrame{DataFrame}}}, Base.var"#6#7"{Pair}}(Base.var"#6#7"{Pair}(), zip(DataFrames.GroupKey{GroupedDataFrame{DataFrame}}[GroupKey: (Species = "Iris-setosa",), GroupKey: (Species = "Iris-versicolor",), GroupKey: (Species = "Iris-virginica",)], GroupedDataFrame with 3 groups based on key: Species
    First Group (50 rows): Species = "Iris-setosa"
    [1m Row [0m│[1m SepalLength [0m[1m SepalWidth [0m[1m PetalLength [0m[1m PetalWidth [0m[1m Species     [0m
    [1m     [0m│[90m Float64     [0m[90m Float64    [0m[90m Float64     [0m[90m Float64    [0m[90m String      [0m
    ─────┼───────────────────────────────────────────────────────────────
       1 │         5.1         3.5          1.4         0.2  Iris-setosa
      ⋮  │      ⋮           ⋮            ⋮           ⋮            ⋮
      50 │         5.0         3.3          1.4         0.2  Iris-setosa
    [36m                                                      48 rows omitted[0m
    ⋮
    Last Group (50 rows): Species = "Iris-virginica"
    [1m Row [0m│[1m SepalLength [0m[1m SepalWidth [0m[1m PetalLength [0m[1m PetalWidth [0m[1m Species        [0m
    [1m     [0m│[90m Float64     [0m[90m Float64    [0m[90m Float64     [0m[90m Float64    [0m[90m String         [0m
    ─────┼──────────────────────────────────────────────────────────────────
       1 │         6.3         3.3          6.0         2.5  Iris-virginica
      ⋮  │      ⋮           ⋮            ⋮           ⋮             ⋮
      50 │         5.9         3.0          5.1         1.8  Iris-virginica
    [36m                                                         48 rows omitted[0m))



`GroupedDataFrame`은 key와 value를 갖는 NamedTuple과 같은 성질을 갖는다고 공식문서에서 설명하고 있다. 그러므로 아래와 같이 indexing을 할 수 있다. 다만 입력하는 값이 왜 이런 형태인지는 모르겠다. 불편할 듯.


```julia
gdf[("Iris-virginica",)]
```




<table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th></tr></thead><tbody><p>50 rows × 5 columns</p><tr><th>1</th><td>6.3</td><td>3.3</td><td>6.0</td><td>2.5</td><td>Iris-virginica</td></tr><tr><th>2</th><td>5.8</td><td>2.7</td><td>5.1</td><td>1.9</td><td>Iris-virginica</td></tr><tr><th>3</th><td>7.1</td><td>3.0</td><td>5.9</td><td>2.1</td><td>Iris-virginica</td></tr><tr><th>4</th><td>6.3</td><td>2.9</td><td>5.6</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>5</th><td>6.5</td><td>3.0</td><td>5.8</td><td>2.2</td><td>Iris-virginica</td></tr><tr><th>6</th><td>7.6</td><td>3.0</td><td>6.6</td><td>2.1</td><td>Iris-virginica</td></tr><tr><th>7</th><td>4.9</td><td>2.5</td><td>4.5</td><td>1.7</td><td>Iris-virginica</td></tr><tr><th>8</th><td>7.3</td><td>2.9</td><td>6.3</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>9</th><td>6.7</td><td>2.5</td><td>5.8</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>10</th><td>7.2</td><td>3.6</td><td>6.1</td><td>2.5</td><td>Iris-virginica</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>




```julia
gdf[[("Iris-virginica",), ("Iris-setosa",)]]
```




<p><b>GroupedDataFrame with 2 groups based on key: Species</b></p><p><i>First Group (50 rows): Species = "Iris-virginica"</i></p><table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th></tr></thead><tbody><tr><th>1</th><td>6.3</td><td>3.3</td><td>6.0</td><td>2.5</td><td>Iris-virginica</td></tr><tr><th>2</th><td>5.8</td><td>2.7</td><td>5.1</td><td>1.9</td><td>Iris-virginica</td></tr><tr><th>3</th><td>7.1</td><td>3.0</td><td>5.9</td><td>2.1</td><td>Iris-virginica</td></tr><tr><th>4</th><td>6.3</td><td>2.9</td><td>5.6</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>5</th><td>6.5</td><td>3.0</td><td>5.8</td><td>2.2</td><td>Iris-virginica</td></tr><tr><th>6</th><td>7.6</td><td>3.0</td><td>6.6</td><td>2.1</td><td>Iris-virginica</td></tr><tr><th>7</th><td>4.9</td><td>2.5</td><td>4.5</td><td>1.7</td><td>Iris-virginica</td></tr><tr><th>8</th><td>7.3</td><td>2.9</td><td>6.3</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>9</th><td>6.7</td><td>2.5</td><td>5.8</td><td>1.8</td><td>Iris-virginica</td></tr><tr><th>10</th><td>7.2</td><td>3.6</td><td>6.1</td><td>2.5</td><td>Iris-virginica</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table><p>&vellip;</p><p><i>Last Group (50 rows): Species = "Iris-setosa"</i></p><table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th></tr></thead><tbody><tr><th>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td><td>Iris-setosa</td></tr><tr><th>7</th><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td><td>Iris-setosa</td></tr><tr><th>8</th><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>9</th><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>10</th><td>4.9</td><td>3.1</td><td>1.5</td><td>0.1</td><td>Iris-setosa</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>



`GroupedDataFrame`에서 key에 사용되지 않은 column을 찾아 함수를 적용할 때는 아래와 같이 `valuecols` 함수를 이용한다.


```julia
combine(gdf, valuecols(gdf) .=> mean)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>SepalLength_mean</th><th>SepalWidth_mean</th><th>PetalLength_mean</th><th>PetalWidth_mean</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th></tr></thead><tbody><p>3 rows × 5 columns</p><tr><th>1</th><td>Iris-setosa</td><td>5.006</td><td>3.418</td><td>1.464</td><td>0.244</td></tr><tr><th>2</th><td>Iris-versicolor</td><td>5.936</td><td>2.77</td><td>4.26</td><td>1.326</td></tr><tr><th>3</th><td>Iris-virginica</td><td>6.588</td><td>2.974</td><td>5.552</td><td>2.026</td></tr></tbody></table>



# Dataframe 형태 변경  Reshaping and turning data

## Reshaping

wide format의 데이터프레임을 long format으로 바꾸고 싶으면 `stack` 함수를 사용한다.


```julia
iris
```




<table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th></tr></thead><tbody><p>150 rows × 5 columns</p><tr><th>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td><td>Iris-setosa</td></tr><tr><th>7</th><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td><td>Iris-setosa</td></tr><tr><th>8</th><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>9</th><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td></tr><tr><th>10</th><td>4.9</td><td>3.1</td><td>1.5</td><td>0.1</td><td>Iris-setosa</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>




```julia
stack(iris, 1:4)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>variable</th><th>value</th></tr><tr><th></th><th>String</th><th>String</th><th>Float64</th></tr></thead><tbody><p>600 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>SepalLength</td><td>5.1</td></tr><tr><th>2</th><td>Iris-setosa</td><td>SepalLength</td><td>4.9</td></tr><tr><th>3</th><td>Iris-setosa</td><td>SepalLength</td><td>4.7</td></tr><tr><th>4</th><td>Iris-setosa</td><td>SepalLength</td><td>4.6</td></tr><tr><th>5</th><td>Iris-setosa</td><td>SepalLength</td><td>5.0</td></tr><tr><th>6</th><td>Iris-setosa</td><td>SepalLength</td><td>5.4</td></tr><tr><th>7</th><td>Iris-setosa</td><td>SepalLength</td><td>4.6</td></tr><tr><th>8</th><td>Iris-setosa</td><td>SepalLength</td><td>5.0</td></tr><tr><th>9</th><td>Iris-setosa</td><td>SepalLength</td><td>4.4</td></tr><tr><th>10</th><td>Iris-setosa</td><td>SepalLength</td><td>4.9</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>



두번째 인자는 long format으로 변할 때 variable과 value column에 모이게 될 column들을 지정해 주는 selector이다. 이 column들은 보통 측정치라고 부른다.  selector로서 column 이름을 직접 주는 것도 가능하다. 이 경우는 `1:4` 대신 `[:SepalLength, :SepalWidth, :PetalLength, :PetalWidth]`를 쓰면 된다.

`stack` 함수의 결과로서 반환되는 DataFrame에는 stack의 대상으로 지정된 column들 이외의 모든 column들도 포함되어 있다.  이 column들을 보통 identifier (id)라고 부른다. 이 column들의 값은 stack column의 값들에 맞추어 반복되는 형태로 나열된다. 

세번째 인자가 주어지면 id column을 지정할 수 있다. 이걸 이용해서 long format으로 만들고 싶은 변수들을 명확하게 지정할 수 있다.


```julia
stack(iris, [:SepalLength, :SepalWidth], :Species)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>variable</th><th>value</th></tr><tr><th></th><th>String</th><th>String</th><th>Float64</th></tr></thead><tbody><p>300 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>SepalLength</td><td>5.1</td></tr><tr><th>2</th><td>Iris-setosa</td><td>SepalLength</td><td>4.9</td></tr><tr><th>3</th><td>Iris-setosa</td><td>SepalLength</td><td>4.7</td></tr><tr><th>4</th><td>Iris-setosa</td><td>SepalLength</td><td>4.6</td></tr><tr><th>5</th><td>Iris-setosa</td><td>SepalLength</td><td>5.0</td></tr><tr><th>6</th><td>Iris-setosa</td><td>SepalLength</td><td>5.4</td></tr><tr><th>7</th><td>Iris-setosa</td><td>SepalLength</td><td>4.6</td></tr><tr><th>8</th><td>Iris-setosa</td><td>SepalLength</td><td>5.0</td></tr><tr><th>9</th><td>Iris-setosa</td><td>SepalLength</td><td>4.4</td></tr><tr><th>10</th><td>Iris-setosa</td><td>SepalLength</td><td>4.9</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>



selector `Not`을 이용하면 id column의 이름 하나와 나머지 모든 column을 variable columnd으로 간단하게 지정할 수 있다.


```julia
stack(iris, Not(:Species))
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>variable</th><th>value</th></tr><tr><th></th><th>String</th><th>String</th><th>Float64</th></tr></thead><tbody><p>600 rows × 3 columns</p><tr><th>1</th><td>Iris-setosa</td><td>SepalLength</td><td>5.1</td></tr><tr><th>2</th><td>Iris-setosa</td><td>SepalLength</td><td>4.9</td></tr><tr><th>3</th><td>Iris-setosa</td><td>SepalLength</td><td>4.7</td></tr><tr><th>4</th><td>Iris-setosa</td><td>SepalLength</td><td>4.6</td></tr><tr><th>5</th><td>Iris-setosa</td><td>SepalLength</td><td>5.0</td></tr><tr><th>6</th><td>Iris-setosa</td><td>SepalLength</td><td>5.4</td></tr><tr><th>7</th><td>Iris-setosa</td><td>SepalLength</td><td>4.6</td></tr><tr><th>8</th><td>Iris-setosa</td><td>SepalLength</td><td>5.0</td></tr><tr><th>9</th><td>Iris-setosa</td><td>SepalLength</td><td>4.4</td></tr><tr><th>10</th><td>Iris-setosa</td><td>SepalLength</td><td>4.9</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>



이에 대한 역변환, 즉 long format에서 wide format으로의 변환은 `unstack` 함수를 이용한다. 이 때 필요한 인자는 id column, column variable 이름, column의 값이 될 column들이 어떤 것인지를 지정하는 것이다.


```julia
iris.id = 1:size(iris, 1)
longdf = stack(iris, Not([:Species, :id]))
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>id</th><th>variable</th><th>value</th></tr><tr><th></th><th>String</th><th>Int64</th><th>String</th><th>Float64</th></tr></thead><tbody><p>600 rows × 4 columns</p><tr><th>1</th><td>Iris-setosa</td><td>1</td><td>SepalLength</td><td>5.1</td></tr><tr><th>2</th><td>Iris-setosa</td><td>2</td><td>SepalLength</td><td>4.9</td></tr><tr><th>3</th><td>Iris-setosa</td><td>3</td><td>SepalLength</td><td>4.7</td></tr><tr><th>4</th><td>Iris-setosa</td><td>4</td><td>SepalLength</td><td>4.6</td></tr><tr><th>5</th><td>Iris-setosa</td><td>5</td><td>SepalLength</td><td>5.0</td></tr><tr><th>6</th><td>Iris-setosa</td><td>6</td><td>SepalLength</td><td>5.4</td></tr><tr><th>7</th><td>Iris-setosa</td><td>7</td><td>SepalLength</td><td>4.6</td></tr><tr><th>8</th><td>Iris-setosa</td><td>8</td><td>SepalLength</td><td>5.0</td></tr><tr><th>9</th><td>Iris-setosa</td><td>9</td><td>SepalLength</td><td>4.4</td></tr><tr><th>10</th><td>Iris-setosa</td><td>10</td><td>SepalLength</td><td>4.9</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>




```julia
unstack(longdf, :id, :variable, :value)
```




<table class="data-frame"><thead><tr><th></th><th>id</th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th></tr><tr><th></th><th>Int64</th><th>Float64?</th><th>Float64?</th><th>Float64?</th><th>Float64?</th></tr></thead><tbody><p>150 rows × 5 columns</p><tr><th>1</th><td>1</td><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td></tr><tr><th>2</th><td>2</td><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td></tr><tr><th>3</th><td>3</td><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td></tr><tr><th>4</th><td>4</td><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td></tr><tr><th>5</th><td>5</td><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td></tr><tr><th>6</th><td>6</td><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td></tr><tr><th>7</th><td>7</td><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td></tr><tr><th>8</th><td>8</td><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td></tr><tr><th>9</th><td>9</td><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td></tr><tr><th>10</th><td>10</td><td>4.9</td><td>3.1</td><td>1.5</td><td>0.1</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>



variable과 value로 지정되는 column 이외의 column들이 unique하다면 (중복되는 경우가 없다면) id 인자는 skip할 수 있다.


```julia
unstack(longdf, :variable, :value)
```




<table class="data-frame"><thead><tr><th></th><th>Species</th><th>id</th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th></tr><tr><th></th><th>String</th><th>Int64</th><th>Float64?</th><th>Float64?</th><th>Float64?</th><th>Float64?</th></tr></thead><tbody><p>150 rows × 6 columns</p><tr><th>1</th><td>Iris-setosa</td><td>1</td><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td></tr><tr><th>2</th><td>Iris-setosa</td><td>2</td><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td></tr><tr><th>3</th><td>Iris-setosa</td><td>3</td><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td></tr><tr><th>4</th><td>Iris-setosa</td><td>4</td><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td></tr><tr><th>5</th><td>Iris-setosa</td><td>5</td><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td></tr><tr><th>6</th><td>Iris-setosa</td><td>6</td><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td></tr><tr><th>7</th><td>Iris-setosa</td><td>7</td><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td></tr><tr><th>8</th><td>Iris-setosa</td><td>8</td><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td></tr><tr><th>9</th><td>Iris-setosa</td><td>9</td><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td></tr><tr><th>10</th><td>Iris-setosa</td><td>10</td><td>4.9</td><td>3.1</td><td>1.5</td><td>0.1</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>



## Turning 또는 pivoting

`AbstractDataFrame`을 회전시키려면 `permutedims`를 이용한다.

>```
>permutedims(df::AbstractDataFrame, src_namescol::Union{Int, Symbol, AbstractString},
>            [dest_namescol::Union{Symbol, AbstractString}];
>            makeunique::Bool=false)
>```
>Turn `df` on its side such that rows become columns and values in the column indexed by `src_namescol` >become the names of new columns. In the resulting DataFrame, column names of `df` will become the first >column with name specified by `dest_namescol`.


```julia
df1 = DataFrame(a=["x", "y"], b=[1.0, 2.0], c=[3, 4], d=[true, false])
```




<table class="data-frame"><thead><tr><th></th><th>a</th><th>b</th><th>c</th><th>d</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Int64</th><th>Bool</th></tr></thead><tbody><p>2 rows × 4 columns</p><tr><th>1</th><td>x</td><td>1.0</td><td>3</td><td>1</td></tr><tr><th>2</th><td>y</td><td>2.0</td><td>4</td><td>0</td></tr></tbody></table>




```julia
permutedims(df1, 1)
```




<table class="data-frame"><thead><tr><th></th><th>a</th><th>x</th><th>y</th></tr><tr><th></th><th>String</th><th>Float64</th><th>Float64</th></tr></thead><tbody><p>3 rows × 3 columns</p><tr><th>1</th><td>b</td><td>1.0</td><td>2.0</td></tr><tr><th>2</th><td>c</td><td>3.0</td><td>4.0</td></tr><tr><th>3</th><td>d</td><td>1.0</td><td>0.0</td></tr></tbody></table>



`permutedims(df1, 1)`의 1은 `df1`의 첫번째 column을 의미한다. 이 열이 새로운 데이터프레임의 column 이름이 된다.

# 정렬 Sort

`sort` 함수를 사용하면 되고, 아래와 같은 형태로 쓰인다.  `rev`에 true가 할당되면 역방향 정렬, `by`에는 값을 비교하기 전에 값에 적용할 함수가 지정된다. 각각의 keyword는 하나의 값, 개별 column에 대응하는 값으로 이루어진 vector 또는 column selector(`:`, `Cols` 등등)가 입력될 수 있다.

Vector 대신 특정 column을 정렬하기 위해서는 `order`를 쓰면 된다. 


```julia
sort(iris, [order(:Species, by=length), order(:SepalLength, rev=true)])
```




<table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th><th>id</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th><th>Int64</th></tr></thead><tbody><p>150 rows × 6 columns</p><tr><th>1</th><td>5.8</td><td>4.0</td><td>1.2</td><td>0.2</td><td>Iris-setosa</td><td>15</td></tr><tr><th>2</th><td>5.7</td><td>4.4</td><td>1.5</td><td>0.4</td><td>Iris-setosa</td><td>16</td></tr><tr><th>3</th><td>5.7</td><td>3.8</td><td>1.7</td><td>0.3</td><td>Iris-setosa</td><td>19</td></tr><tr><th>4</th><td>5.5</td><td>4.2</td><td>1.4</td><td>0.2</td><td>Iris-setosa</td><td>34</td></tr><tr><th>5</th><td>5.5</td><td>3.5</td><td>1.3</td><td>0.2</td><td>Iris-setosa</td><td>37</td></tr><tr><th>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td><td>Iris-setosa</td><td>6</td></tr><tr><th>7</th><td>5.4</td><td>3.7</td><td>1.5</td><td>0.2</td><td>Iris-setosa</td><td>11</td></tr><tr><th>8</th><td>5.4</td><td>3.9</td><td>1.3</td><td>0.4</td><td>Iris-setosa</td><td>17</td></tr><tr><th>9</th><td>5.4</td><td>3.4</td><td>1.7</td><td>0.2</td><td>Iris-setosa</td><td>21</td></tr><tr><th>10</th><td>5.4</td><td>3.4</td><td>1.5</td><td>0.4</td><td>Iris-setosa</td><td>32</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>




```julia
sort(iris, [:Species, :PetalLength], rev=(true, false))
```




<table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th><th>id</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th><th>Int64</th></tr></thead><tbody><p>150 rows × 6 columns</p><tr><th>1</th><td>4.9</td><td>2.5</td><td>4.5</td><td>1.7</td><td>Iris-virginica</td><td>107</td></tr><tr><th>2</th><td>6.2</td><td>2.8</td><td>4.8</td><td>1.8</td><td>Iris-virginica</td><td>127</td></tr><tr><th>3</th><td>6.0</td><td>3.0</td><td>4.8</td><td>1.8</td><td>Iris-virginica</td><td>139</td></tr><tr><th>4</th><td>5.6</td><td>2.8</td><td>4.9</td><td>2.0</td><td>Iris-virginica</td><td>122</td></tr><tr><th>5</th><td>6.3</td><td>2.7</td><td>4.9</td><td>1.8</td><td>Iris-virginica</td><td>124</td></tr><tr><th>6</th><td>6.1</td><td>3.0</td><td>4.9</td><td>1.8</td><td>Iris-virginica</td><td>128</td></tr><tr><th>7</th><td>5.7</td><td>2.5</td><td>5.0</td><td>2.0</td><td>Iris-virginica</td><td>114</td></tr><tr><th>8</th><td>6.0</td><td>2.2</td><td>5.0</td><td>1.5</td><td>Iris-virginica</td><td>120</td></tr><tr><th>9</th><td>6.3</td><td>2.5</td><td>5.0</td><td>1.9</td><td>Iris-virginica</td><td>147</td></tr><tr><th>10</th><td>5.8</td><td>2.7</td><td>5.1</td><td>1.9</td><td>Iris-virginica</td><td>102</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>




```julia
sort(iris, [order(:Species, rev=true), :PetalLength])
```




<table class="data-frame"><thead><tr><th></th><th>SepalLength</th><th>SepalWidth</th><th>PetalLength</th><th>PetalWidth</th><th>Species</th><th>id</th></tr><tr><th></th><th>Float64</th><th>Float64</th><th>Float64</th><th>Float64</th><th>String</th><th>Int64</th></tr></thead><tbody><p>150 rows × 6 columns</p><tr><th>1</th><td>4.9</td><td>2.5</td><td>4.5</td><td>1.7</td><td>Iris-virginica</td><td>107</td></tr><tr><th>2</th><td>6.2</td><td>2.8</td><td>4.8</td><td>1.8</td><td>Iris-virginica</td><td>127</td></tr><tr><th>3</th><td>6.0</td><td>3.0</td><td>4.8</td><td>1.8</td><td>Iris-virginica</td><td>139</td></tr><tr><th>4</th><td>5.6</td><td>2.8</td><td>4.9</td><td>2.0</td><td>Iris-virginica</td><td>122</td></tr><tr><th>5</th><td>6.3</td><td>2.7</td><td>4.9</td><td>1.8</td><td>Iris-virginica</td><td>124</td></tr><tr><th>6</th><td>6.1</td><td>3.0</td><td>4.9</td><td>1.8</td><td>Iris-virginica</td><td>128</td></tr><tr><th>7</th><td>5.7</td><td>2.5</td><td>5.0</td><td>2.0</td><td>Iris-virginica</td><td>114</td></tr><tr><th>8</th><td>6.0</td><td>2.2</td><td>5.0</td><td>1.5</td><td>Iris-virginica</td><td>120</td></tr><tr><th>9</th><td>6.3</td><td>2.5</td><td>5.0</td><td>1.9</td><td>Iris-virginica</td><td>147</td></tr><tr><th>10</th><td>5.8</td><td>2.7</td><td>5.1</td><td>1.9</td><td>Iris-virginica</td><td>102</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>


