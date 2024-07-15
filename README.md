# windows-tricks

Данный репозиторий представляет собой набор твиков или советов от пользователя перешедшего с linux на windows.

Создание директории и добавление её в path в powershell:
```
Function Add-PathVariable {
    param (
        [string]$addPath
    )
    if (Test-Path $addPath){
        $regexAddPath = [regex]::Escape($addPath)
        $arrPath = $env:Path -split ';' | Where-Object {$_ -notMatch 
"^$regexAddPath\\?"}
        $env:Path = ($arrPath + $addPath) -join ';'
    } else {
        Throw "'$addPath' is not a valid path."
    }
}

Add-PathVariable C:\Users\username\bin
```
Это добавит в переменную path папку bin в корневом каталоге вашего пользователя

Поиск по предидущим коммандам по префиксу как это реализовано например в zsh + oh-my-zsh:
```
Set-PSReadLineOption -HistorySearchCursorMovesToEnd
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
```

Установите winget, а после oh-my-posh командой `winget install oh-my-posh` Если выведет несколько вариантов вы можете скопировать ID нужного продукта и заменить им название пакета

`oh-my-posh init pwsh --config $env:POSH_THEMES_PATH/bubbles.omp.json | Invoke-Expression`

Данная команда добавленная в powershell profile Запустит oh-my-posh с темой из указанного файла

Директорию `~/.config`, зачастую замещает директория `~\AppData\Local`

Для отклюмения стандартного вывода powershell, например:
```
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Установите последнюю версию PowerShell для новых функций и улучшения! https://aka.ms/PSWindows
```
Запустите powershell с ключём `-nologo`, например я использую виндовс терминал и сессию powershell, там можно указать команду запуска сессии, пример: `%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -nologo`
