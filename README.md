# PHP_Recursion
Пример рекурсивной обработки массива с неизвестной глубиной

## Имеем массив вида
Глубина неизвестна

```code
Array
(
    [ID] => 968
    [NAME] => name1
    [DEPTH_LEVEL] => 1
    [CHILD] => Array
        (
            [969] => Array
                (
                    [ID] => 969
                    [NAME] => name969
                    [DEPTH_LEVEL] => 2
                )

            [970] => Array
                (
                    [ID] => 970
                    [NAME] => name970
                    [DEPTH_LEVEL] => 2
                    [CHILD] => Array
                      (
                        ...
                      )
                )

        )

```


## Функция обработки массива неизвестной глубины по ключу [CHILD]
```php
	function recursiveMassive($arr, $refresher=false) {
		$padding = 25;
		if(!$refresher) {
			echo '<div class="company___section" data-id="'.$arr[ID].'" style="margin-left: '.($padding*$arr[DEPTH_LEVEL]).'px;">'.$arr[NAME].'</div>';
		}
		if(array_key_exists('CHILD', $arr)) {
			foreach ($arr[CHILD] as $key => $section) {

				echo '<div class="company_section" data-id="'.$arr[ID].'" style="margin-left: '.($padding*$section[DEPTH_LEVEL]).'px;">'.$section[NAME].'</div>';
				if(array_key_exists('CHILD', $section)) {
					recursiveMassive($section, 1);
				}
			}
		}
	}
  ```
  
  Данная функция выводит строки с помощью echo и делает отступы (margin-left). В данных местах можно подстраивать функцию под ваши требования
  Условие <b>refresher</b> проверяет, подраздел это или родительский раздел.

### Примерный вид вывода данного массива:
```
name1
  name969
  name970
      namexxx
        namexxx
        namexxx
      namexxx
  namexxx
    namexx
```
  
  
