# ๐ฅฝ Observable(๊ด์ฐฐ ๊ฐ๋ฅํ)

### observalble ์ด๋?

- Rx์ ์ฌ์ฅ
- `observable` = `observable sequence` = `sequence` : ๊ฐ๊ฐ์ ๋จ์ด๋ฅผ ๊ณ์ ๋ณด๊ฒ ๋ ๊ฑด๋ฐ ๋ค ๊ฐ์๋ง์ด๋ค.
- ์ฌ๊ธฐ์๋ ๋ชจ๋ ๊ฒ์ด ๋น๋๊ธฐ์ (asynchronous)์ด๋ค.
- Observable ๋ค์ ์ผ์  ๊ธฐ๊ฐ ๋์ ๊ณ์ํด์ ์ด๋ฒคํธ๋ฅผ ์์ฑํ๋ฉฐ, ์ด๋ฌ๋ง ๊ณผ์ ์ ๋ณดํต **emitting(๋ฐฉ์ถ)**์ด๋ผ๊ณ  ํํํ๋ค.
- ๊ฐ๊ฐ์ ์ด๋ฒคํธ๋ค์ ์ซ์๋ ์ปค์คํํ ์ธ์คํด์ค ๋ฑ๊ณผ ๊ฐ์ ๊ฐ์ ๊ฐ์ง ์ ์์ผ๋ฉฐ, ๋๋ ํญ๊ณผ ๊ฐ์ ์ ์ค์ฒ๋ฅผ ์ธ์ํ  ์๋ ์๋ค.

### Observable์ ์๋ช์ฃผ๊ธฐ

![https://raw.githubusercontent.com/fimuxd/RxSwift/master/Lectures/02_Observables/1. marble.png](https://raw.githubusercontent.com/fimuxd/RxSwift/master/Lectures/02_Observables/1.%20marble.png)

- next ์ด๋ฒคํธ๋ฅผ ํตํด ๊ฐ๊ฐ์ ์์๋ฅผ ๋ฐฉ์ถํ๋ ๊ฒ

![https://raw.githubusercontent.com/fimuxd/RxSwift/master/Lectures/02_Observables/2. lifecycle1.png](https://raw.githubusercontent.com/fimuxd/RxSwift/master/Lectures/02_Observables/2.%20lifecycle1.png)

- ์ด Observable์ ์ ๊ฐ์ tap ์ด๋ฒคํธ๋ฅผ ๋ฐฉ์ถํ ๋ค ์์  ๋๋ฃ๋จ. ์ด๊ฒ์ด completed ์ด๋ฒคํธ์ด๋ค.

![https://raw.githubusercontent.com/fimuxd/RxSwift/master/Lectures/02_Observables/3. lifecycle2.png](https://raw.githubusercontent.com/fimuxd/RxSwift/master/Lectures/02_Observables/3.%20lifecycle2.png)

- ์๋จ์ ์์๋ค๊ณผ ๋ค๋ฅธ๊ฒ ์๋ฌ๊ฐ ๋ฐ์ํ๊ฒ์ด๋ค.
- Observable์ด ์์  ์ข๋ฃ๋์๋ค๋ ๋ฉด์ ๊ฐ์ง๋ง, `error` ์ด๋ฒคํธ๋ฅผ ํตํด ์ข๋ฃ๋ ๊ฒ์ด๋ค.

### Observalble ๋ง๋ค๊ธฐ

1. just, of, from

   1. **just**

      ```swift
      let one = 1
      let two = 2
      let three = 3
      
      let observable: Observable<Int> = Observable<Int>.just(one)
      ```

      - one ์ ์๋ฅผ ์ด์ฉํ์ฌ just method๋ฅผ ํตํด Int ํ์์ Observable sequence๋ฅผ ๋ง๋๋ ์ฝ๋์ด๋ค.
      - `just` ๋ `Observable`์ ํ์ ๋ฉ์๋๋ก์ ์ด๋ฆ์์ ์ถ์ธกํ  ์ ์๋ฏ์ด ์ค์ง ํ๋์ ์์๋ฅผ ํฌํจํ๋ Observable sequence๋ฅผ ์์ฑํ๋ค.

   2. **of**

      ```swift
      let observable2 = Observable.of(one, two, three)
      ```

      - `of`์ฐ์ฐ์๋ ์ฃผ์ด์ง ๊ฐ๋ค์ **ํ์ ์ถ๋ก **์ ํตํด Observable sequence๋ฅผ ์์ฑํ๋ค.
      - ๊ทธ๋์ `observable2`์ ํ์์ `Observable<Int>`๋ก ํ์์ด ๋๋ค.
      - ๋ฐ๋ผ์ ์ด๋ค array๋ฅผ Observable array๋ก ๋ง๋ค๊ณ  ์ถ๋ค๋ฉด, array๋ฅผ `of`์ฐ์ฐ์์ ์ง์ด ๋ฃ์ผ๋ฉด ๋๋ค.

      ```swift
      let observable3 = Observable.of([one, two, three])
      ```

      - observable3์ ํ์์ Observable<[Int]>
      - ์ด๋ ๊ฒ ํ๋ฉด `just`์ฐ์ฐ์๋ฅผ ์ด๊ฒ๊ณผ ๊ฐ์ด [1, 2, 3]์ **๋จ์ผ์์**๋ก ๊ฐ์ง๊ฒ ๋๋ค.

   3. **from**

      ```swift
      let observable4 = Observable.from([one, two, three])
      ```

      - observable4์ ํ์์ `Observable<Int>`
      - from ์ฐ์ฐ์๋ ์ผ๋ฐ์ ์ธ **array ๊ฐ๊ฐ ์์๋ค์ ํ๋์ฉ** ๋ฐฉ์ถํ๋ค
      - from ์ฐ์ฐ์๋ **์ค์ง array**๋ง ์ฌ์ฉํ๋ค

### Observable ๊ตฌ๋

- Observable ์ค์ ๋ก sequence ์ ์์ผ ๋ฟ์ด๋ค. Observable์ subscribe, ์ฆ ๊ตฌ๋๋๊ธฐ ์ ์๋ ์๋ฌด๋ฐ ์ด๋ฒคํธํ  ๋ณด๋ด์ง ์๋๋ค. **๊ทธ์  ์ ์**์ผ ๋ฟ์ด๋ค.

1. **.subscribe()**

   ```swift
   let one = 1
   let two = 2
   let three = 3
   
   let observable = Observable.of(one, two, three)
   	observable.subscribe({ (event) in
   			 print(event)
   		})
    	
    	/* Prints:
    	 next(1)
    	 next(2)
    	 next(3)
    	 completed
    	*/
   ```

   - .subscribe๋ escaping ํด๋ก์ ๋ก `Int`ํ์์ `Event`๋ก ๊ฐ๋๋ค. escaping์ ๋ํ ๋ฆฌํด๊ฐ์ ์์ผ๋ฉฐ `.subscribe`์ `Disposable`์ ๋ฆฌํดํ๋ค.
   - ํ๋ฆฐํธ๋ ๊ฐ์ ๋ณด๋ฉด, Observable์
     - 1. ๊ฐ๊ฐ์ ์์๋ค์ ๋ํด `.next` ์ด๋ฒคํธ๋ฅผ ๋ฐฉ์ถํ๋ค.
     - 1. ์ต์ข์ ์ผ๋ก `.completed`๋ฅผ ๋ฐฉ์ถํ๋ค.
   - Observable์ ์ด์ฉํ๋ค๋ณด๋ฉด, ๋๋ถ๋ถ์ ๊ฒฝ์ฐ Observable์ด `.next`์ด๋ฒคํธ๋ฅผ ํตํด ๋ฐฉ์ถํ๋ ์์์ ๊ฐ์ฅ ๊ด์ฌ๊ฐ์ง๊ฒ ๋  ๊ฒ์ด๋ค.

2. **subscribe(onNext:)**

   - ์๊ธฐ์ ์ฝ๋๋ฅผ ๋ค์๊ณผ ๊ฐ์ด ๋ฐ๊ฟ๋ณด๋ฉด

   ```swift
   observable.subscribe { event in
    	if let element = event.element {
    		print(element)
    	}
    }
    
    /* Prints:
     1
     2
     3
    */
   ```

   - ์์ฃผ ์์ฃผ ์ฐ์ด๋ ํจํด์ด๊ธฐ ๋๋ฌธ์ RxSwift์๋ ์ด ๋ถ๋ถ์ ๋ํ ์ฃฝ์ฝํ๋ค์ด ์๋ค.
   - ์ฆ, Observable์ด ๋ฐฉํํ๋ `.next`, `.error`, `.completed` ๊ฐ์ ๊ฐ๊ฐ์ ์ด๋ฒคํธ๋ค์ ๋ํด `subscribe` ์ฐ์ฐ์๊ฐ ์๋ค.

   ```swift
   observable.subscribe(onNext: { (element) in
    	print(element)
    })
    
    /* Prints:
     1
     2
     3
    */
   ```

   - `.onNext` ํด๋ก์ ๋ `.next`์ด๋ฒคํธ๋ง์ argument๋ก ์ทจํ ๋ค ํธ๋ค๋งํ  ๊ฒ์ด๊ณ , ๋ค๋ฅธ ๊ฒ๋ค์ ๋ชจ๋ ๋ฌด์ํ๊ฒ ๋๋ค.
