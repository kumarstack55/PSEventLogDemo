# PSEventLogDemo

## 要件

- Microsoft Windows 10+
- PowerShell 5.1+

## LogName の一覧を得る

```powershell
Get-EventLog -List |
Format-Table Log
```

## Source の一覧を得る

```powershell
Get-EventLog -LogName Application |
Select-Object -Property Source -Unique |
Sort-Object -Property Source
```

## Source を追加する

```powershell
# powershell.exe を管理者権限で実行
New-EventLog -LogName Application -Source MySource
```

## Source を消す

```powershell
# powershell.exe を管理者権限で実行
Remove-EventLog -Source MySource
```

Source は消えるが、 Write-EventLog で記録したログは消えない。

## イベント一覧を参照する

### ウィンドウでイベント一覧を参照する

イベント ビューアーを起動する。

```
eventvwr.exe
```

- Windows ログ
    - Application
        - 現在のログをフィルター
            - イベント ソース: MySource
            - `[OK]`

### コマンドラインでイベント一覧を参照する

```powershell
Get-EventLog -LogName Application -Source MySource
```

## イベント ログを追加する

```powershell
Write-EventLog -LogName Application -Source MySource -EventId 1 -EntryType Information -Message "test"
```

## 参考資料

- About Event Logging
    - https://learn.microsoft.com/en-us/windows/win32/eventlog/about-event-logging
- Get-EventLog
    - https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-eventlog?view=powershell-5.1
