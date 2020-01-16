# SIGBUS 에러
주소는 valid하지만 접근 못하는 경우도 있습니다.
(인텔 cpu는 cpu적으로 이걸 해결한다고는 들었지만 다른cpu는 
잘 모르겠군요)
memory에서 register로 데이터를 가져올때 보통 4바이트 단위로
가지오게 되어 있으며 memory는 4의 배수단위로 접근해야 합니다.
즉 0-3 번지, 4-7번지, 8-12번지 이런식으로 접근하게 되져
그런데 만약 6-9번지를 접근하게 되면 버스에러가 발생하게 됩니다.
왜냐하면 1번의 메모리 접근으로는 6-9번지에 있는 데이터를 접근할수
없기 때문이져. 물론 cpu에서 이를 해결할 수 있습니다. 그거야 cpu
맘이구...
일단 위와 같은 경우도 버스에러가 난다고 알고있습니다.
 
 
해결책
 
1. 구조체를 선언했을때 sigbus가 발생할 경우
padding과 packing을 하면된다.
https://ohhosk.tistory.com/85

## SIGBUS에러를 catch하는 법
https://stackoverflow.com/questions/28124154/how-to-catch-sigbus-error
