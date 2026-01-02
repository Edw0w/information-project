# information-project


teste
<img width="999" height="633" alt="Captura de tela 2026-01-02 010703" src="https://github.com/user-attachments/assets/fb97be5c-bc80-4c4b-afb0-6037d1c1dd3d" />

<img width="1074" height="403" alt="image" src="https://github.com/user-attachments/assets/f14ebff4-4a4c-4f01-8300-73d00adff344" />



MACRO (1): 
Sub CadUsua()

With Sheets("BASE-USUARIO")
    If Application.WorksheetFunction.CountA(.Range("d3:d1048576")) = 0 Then
    proxID = 1
Else
    proxID = WorksheetFunction.Max(.Range("d3:d1048576")) + 1
End If

.Range("D3:R3").Insert Shift:=xlDown

.Range("D3").Value = proxID

    .Range("E3").Value = Sheets("CADASTRO-CLIENTE").Range("D7").Value
    .Range("F3").Value = Sheets("CADASTRO-CLIENTE").Range("D10").Value
    .Range("G3").Value = Sheets("CADASTRO-CLIENTE").Range("D13").Value
    .Range("H3").Value = Sheets("CADASTRO-CLIENTE").Range("G13").Value
    .Range("I3").Value = Sheets("CADASTRO-CLIENTE").Range("D16").Value
    .Range("J3").Value = Sheets("CADASTRO-CLIENTE").Range("D19").Value
    .Range("K3").Value = Sheets("CADASTRO-CLIENTE").Range("G19").Value
    .Range("L3").Value = Sheets("CADASTRO-CLIENTE").Range("D22").Value
    .Range("M3").Value = Sheets("CADASTRO-CLIENTE").Range("G22").Value
    .Range("N3").Value = Sheets("CADASTRO-CLIENTE").Range("D25").Value
    .Range("O3").Value = Sheets("CADASTRO-CLIENTE").Range("D28").Value
    .Range("P3").Value = Sheets("CADASTRO-CLIENTE").Range("D31").Value
    .Range("Q3").Value = Sheets("CADASTRO-CLIENTE").Range("D34").Value
    
    .Range("c3").Value = Now
    .Range("c3").NumberFormat = "dd/mm/yyyy hh:mm:ss"
    
End With
End Sub

Sub cadEmpresa()

With Sheets("BASE-EMPRESA")
    If Application.WorksheetFunction.CountA(.Range("C4:C1048576")) = 0 Then
    proxID = 1
Else
    proxID = WorksheetFunction.Max(.Range("C4:C1048576")) + 1
End If

.Range("B4:Q4").Insert Shift:=xlDown

.Range("C4").Value = proxID

    .Range("D4").Value = Sheets("CADASTRO-EMPRESA").Range("D7").Value
    .Range("E4").Value = Sheets("CADASTRO-EMPRESA").Range("D10").Value
    .Range("F4").Value = Sheets("CADASTRO-EMPRESA").Range("D13").Value
    .Range("G4").Value = Sheets("CADASTRO-EMPRESA").Range("D16").Value
    .Range("H4").Value = Sheets("CADASTRO-EMPRESA").Range("D19").Value
    .Range("I4").Value = Sheets("CADASTRO-EMPRESA").Range("H19").Value
    .Range("J4").Value = Sheets("CADASTRO-EMPRESA").Range("D22").Value
    .Range("K4").Value = Sheets("CADASTRO-EMPRESA").Range("H22").Value
    .Range("L4").Value = Sheets("CADASTRO-EMPRESA").Range("D25").Value
    .Range("M4").Value = Sheets("CADASTRO-EMPRESA").Range("D28").Value
    .Range("N4").Value = Sheets("CADASTRO-EMPRESA").Range("D31").Value
    .Range("O4").Value = _
    IIf(Sheets("CADASTRO-EMPRESA").Range("D35").Value = True, "Moto; ", "") & _
    IIf(Sheets("CADASTRO-EMPRESA").Range("E35").Value = True, "Carro; ", "") & _
    IIf(Sheets("CADASTRO-EMPRESA").Range("F35").Value = True, "Van; ", "") & _
    IIf(Sheets("CADASTRO-EMPRESA").Range("G35").Value = True, "Transportadora", "")
    
    .Range("P4").Value = Sheets("CADASTRO-EMPRESA").Range("D38").Value
    .Range("Q4").Value = Sheets("CADASTRO-EMPRESA").Range("D41").Value
    
    .Range("B4").Value = Now
    .Range("B4").NumberFormat = "dd/mm/yyyy hh:mm:ss"
    
End With
End Sub


Sub abreLog()
    FormTipoLog.Show
End Sub

Sub abreCad()
    FormTipoCad.Show
End Sub

Sub Saircont()
    Sheets("MERCADO-LOGADO").Range("S1").MergeArea.ClearContents
    Sheets("CARRINHO-LOGADO").Range("S1").MergeArea.ClearContents
    Sheets("MERCADO-INICIAL").Activate
End Sub

Sub LogUsu()
    FormUsuario.Show
End Sub

Sub LogEmp()
    FormEmpresa.Show
End Sub

Sub IrCarrinho()
    Sheets("CARRINHO-LOGADO").Activate
End Sub


Sub AdCarrinho()
    produtoID = Split(Application.Caller, "_")(1)
    
    Set cel = Sheets("tabela-produtos").Columns("B").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
        
    If cel Is Nothing Then
        MsgBox "Produto não encontrado"
        Exit Sub
    End If
        
    linhaProduto = cel.Row
    
    Set celCarrinho = Sheets("CARRINHO-LOGADO").Columns("D").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
        
    If Not celCarrinho Is Nothing Then
        celCarrinho.Offset(0, 6).Value = celCarrinho.Offset(0, 6).Value + 1
        celCarrinho.Offset(0, 10).Formula = _
            "=L" & celCarrinho.Row & "*J" & celCarrinho.Row
            
    Else
        linhaCarrinho = Sheets("CARRINHO-LOGADO").Cells(Rows.Count, 4).End(xlUp).Row + 1
    
    Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 4).Value = Sheets("tabela-produtos").Cells(linhaProduto, 2).Value
    Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 6).Value = Sheets("tabela-produtos").Cells(linhaProduto, 3).Value
    Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 8).Value = Sheets("tabela-produtos").Cells(linhaProduto, 8).Value
    Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 10).Value = 1
    Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 12).Value = Sheets("tabela-produtos").Cells(linhaProduto, 7).Value
    Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 14).Formula = "=L" & linhaCarrinho & "*J" & linhaCarrinho
    
    
    

    
    
    End If
    
    MsgBox "Produto adicionado ao carrinho!"
    With Sheets("CARRINHO-LOGADO")
    .Range("U16").Value = Application.Sum(.Range("N5:N" & .Rows.Count))
End With






End Sub


Sub CompraProd()
    nomeBotao = Application.Caller
    
    If InStr(nomeBotao, "_") = 0 Then
        MsgBox "Botao sem ID de produto"
        Exit Sub
    End If
    
    produtoID = Split(nomeBotao, "_")(1)
    
    Set cel = Sheets("tabela-produtos").Columns("B").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
        
    If cel Is Nothing Then
        MsgBox "Produto nao encontrado"
        Exit Sub
    End If
    
    linhaProduto = cel.Row
    
    Set celCarrinho = Sheets("CARRINHO-LOGADO").Columns("D").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
    
    If Not celCarrinho Is Nothing Then
        celCarrinho.Offset(0, 6).Value = celCarrinho.Offset(0, 6).Value + 1
        celCarrinho.Offset(0, 10).Formula = _
            "=L" & celCarrinho.Row & "*J" & celCarrinho.Row
    Else
            linhaCarrinho = Sheets("CARRINHO-LOGADO").Cells( _
                Sheets("CARRINHO-LOGADO").Rows.Count, 4).End(xlUp).Row + 1
                
                Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 4).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 2).Value
                
                Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 6).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 3).Value
    
                Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 8).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 8).Value
                
                Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 10).Value = _
                1
                
                Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 12).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 7).Value
                
                Sheets("CARRINHO-LOGADO").Cells(linhaCarrinho, 14).Value = _
                    "=L" & linhaCarrinho & "*J" & linhaCarrinho
                
         End If
         
         
         
         
         
         
         
         With Sheets("CARRINHO-LOGADO")
            .Range("U16").Value = Application.Sum(.Range("N5:N" & .Rows.Count))
         End With

         Sheets("CARRINHO-LOGADO").Activate
                
End Sub



Sub escoTransporte()

    ' Calcula o peso total (peso unitário x quantidade)
    pesoTotal = Application.WorksheetFunction.SumProduct( _
        Sheets("CARRINHO-LOGADO").Range("H5:H100"), Sheets("CARRINHO-LOGADO").Range("J5:J100"))
    
    ' Verifica se existe produto de alto risco pelo ID
    riscoAlto = False
    
    ' Percorre todas as linhas da coluna D (IDs do carrinho)
    For linha = 5 To 100
        idCarrinho = Sheets("CARRINHO-LOGADO").Cells(linha, "D").Value
        
        If idCarrinho <> "" Then
            On Error Resume Next
            risco = Application.WorksheetFunction.VLookup(idCarrinho, _
                        Sheets("tabela-produtos").Range("B3:M42"), 12, False)
            On Error GoTo 0
            
            If risco = "Alto" Then
                riscoAlto = True
                Exit For   ' já achou um produto de risco alto, não precisa continuar
            End If
        End If
    Next linha
    
    ' Regras de transporte
    If pesoTotal > 6 Or riscoAlto = True Then
        opcIncompleta.Show
    Else
        opcCompleta.Show
    End If
End Sub


Sub AdCarrinhoSem()
    produtoID = Split(Application.Caller, "_")(1)
    
    Set cel = Sheets("tabela-produtos").Columns("B").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
        
    If cel Is Nothing Then
        MsgBox "Produto não encontrado"
        Exit Sub
    End If
        
    linhaProduto = cel.Row
    
    Set celCarrinho = Sheets("CARRINHO-SEM").Columns("D").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
        
    If Not celCarrinho Is Nothing Then
        celCarrinho.Offset(0, 6).Value = celCarrinho.Offset(0, 6).Value + 1
        celCarrinho.Offset(0, 10).Formula = _
            "=L" & celCarrinho.Row & "*J" & celCarrinho.Row
            
    Else
        linhaCarrinho = Sheets("CARRINHO-SEM").Cells(Rows.Count, 4).End(xlUp).Row + 1
    
    Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 4).Value = Sheets("tabela-produtos").Cells(linhaProduto, 2).Value
    Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 6).Value = Sheets("tabela-produtos").Cells(linhaProduto, 3).Value
    Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 8).Value = Sheets("tabela-produtos").Cells(linhaProduto, 8).Value
    Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 10).Value = 1
    Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 12).Value = Sheets("tabela-produtos").Cells(linhaProduto, 7).Value
    Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 14).Formula = "=L" & linhaCarrinho & "*J" & linhaCarrinho
    
    
    

    
    
    End If
    
    MsgBox "Produto adicionado ao carrinho!"
    With Sheets("CARRINHO-SEM")
    .Range("U16").Value = Application.Sum(.Range("N5:N" & .Rows.Count))
End With


        
                
                    ' ESCRENDO O CODIGO Calcula o peso total (peso unitário x quantidade)
                    pesoTotal = Application.WorksheetFunction.SumProduct( _
                        Sheets("CARRINHO-LOGADO").Range("H5:H100"), Sheets("CARRINHO-LOGADO").Range("J5:J100"))
                    
                    ' Verifica se existe produto de alto risco pelo ID
                    riscoAlto = False
                    
                    ' Percorre todas as linhas da coluna D (IDs do carrinho)
                    For linha = 5 To 100
                        idCarrinho = Sheets("CARRINHO-LOGADO").Cells(linha, "D").Value
                        
                        If idCarrinho <> "" Then
                            On Error Resume Next
                            risco = Application.WorksheetFunction.VLookup(idCarrinho, _
                                        Sheets("tabela-produtos").Range("B3:M42"), 12, False)
                            On Error GoTo 0
                            
                            If risco = "Alto" Then
                                riscoAlto = True
                                Exit For   ' já achou um produto de risco alto, não precisa continuar
                            End If
                        End If
                    Next linha
                    
                    ' Regras de transporte
                    If pesoTotal > 6 Or riscoAlto = True Then
                        opcIncompleta.Show
                    Else
                        opcCompleta.Show
                    End If
                
                





End Sub


Sub CompraProdSem()
    nomeBotao = Application.Caller
    
    If InStr(nomeBotao, "_") = 0 Then
        MsgBox "Botao sem ID de produto"
        Exit Sub
    End If
    
    produtoID = Split(nomeBotao, "_")(1)
    
    Set cel = Sheets("tabela-produtos").Columns("B").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
        
    If cel Is Nothing Then
        MsgBox "Produto nao encontrado"
        Exit Sub
    End If
    
    linhaProduto = cel.Row
    
    Set celCarrinho = Sheets("CARRINHO-SEM").Columns("D").Find( _
        What:=produtoID, LookIn:=xlValues, LookAt:=xlWhole)
    
    If Not celCarrinho Is Nothing Then
        celCarrinho.Offset(0, 6).Value = celCarrinho.Offset(0, 6).Value + 1
        celCarrinho.Offset(0, 10).Formula = _
            "=L" & celCarrinho.Row & "*J" & celCarrinho.Row
    Else
            linhaCarrinho = Sheets("CARRINHO-SEM").Cells( _
                Sheets("CARRINHO-SEM").Rows.Count, 4).End(xlUp).Row + 1
                
                Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 4).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 2).Value
                
                Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 6).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 3).Value
    
                Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 8).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 8).Value
                
                Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 10).Value = _
                1
                
                Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 12).Value = _
                Sheets("tabela-produtos").Cells(linhaProduto, 7).Value
                
                Sheets("CARRINHO-SEM").Cells(linhaCarrinho, 14).Value = _
                    "=L" & linhaCarrinho & "*J" & linhaCarrinho
                
         End If
         
         
         
         
         
         
         
         With Sheets("CARRINHO-SEM")
            .Range("U16").Value = Application.Sum(.Range("N5:N" & .Rows.Count))
         End With

         Sheets("CARRINHO-SEM").Activate
                
End Sub




<img width="1364" height="781" alt="image" src="https://github.com/user-attachments/assets/abb94540-2a5f-4a65-ad56-5b3e3325e61f" />


<img width="1392" height="839" alt="image" src="https://github.com/user-attachments/assets/4f4e871d-4850-4850-b590-72f61ed13d2c" />

<img width="1417" height="807" alt="image" src="https://github.com/user-attachments/assets/c3551532-7986-40e0-99a5-f56cdd25fc81" />


<img width="1458" height="827" alt="image" src="https://github.com/user-attachments/assets/06be53ad-5144-488e-a4b6-0ed37d504c5a" />

<img width="1488" height="796" alt="image" src="https://github.com/user-attachments/assets/bd2c43bc-eb56-4590-baa4-17ea0d5a702a" />


