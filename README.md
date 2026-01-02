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

<img width="1464" height="790" alt="image" src="https://github.com/user-attachments/assets/dafd34e8-4109-4ceb-be19-111a72374259" />

<img width="1298" height="796" alt="image" src="https://github.com/user-attachments/assets/97825f57-1554-4c60-ba48-4fd731a50bd4" />

<img width="1224" height="796" alt="image" src="https://github.com/user-attachments/assets/928d2fe4-6a9d-4326-a3cd-5609c9ce5ad6" />

<img width="1856" height="812" alt="image" src="https://github.com/user-attachments/assets/28bbe207-2157-43d6-ad0c-daa36a360d14" />

<img width="1911" height="797" alt="image" src="https://github.com/user-attachments/assets/b03006b6-82c9-4d4b-b075-a11c2820c2cb" />

<img width="1892" height="801" alt="image" src="https://github.com/user-attachments/assets/8af994c7-3f68-4176-8888-dce15a1f05cf" />

<img width="1990" height="1515" alt="image" src="https://github.com/user-attachments/assets/9ac080b5-66e6-4829-9d95-25594295f205" />

PRODUTOS DO MERCADO ONLINE												
ID_PRODUTO	NOME	IMAGEM	DESCRICAO	QTDE_PRODUTO	VALOR(R$)	PESO(em kg)	Unidade (Líquido/Peso)	COMPLEMENTO_PESO	ID_EMPRESA	DONO_MERCADO	RISCO	ESTOQUE
1	Arroz Integral 1kg		Grão longo, rico em fibras	1	 R$ 8,90 	1,00	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	23
2	Feijão Carioca 1kg		Tradicional, sabor marcante	1	 R$ 7,50 	1,00	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	25
3	Açúcar Refinado 1kg		Açúcar branco cristalizado	1	 R$ 5,10 	1,00	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	2
4	Sal Refinado 1kg		Sal de cozinha refinado	1	 R$ 3,20 	1,00	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	45
5	Macarrão Espaguete 500g		Massa tradicional para molhos	1	 R$ 4,70 	0,50	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	12
6	Farinha de Trigo 1kg		Base para pães, bolos e massas	1	 R$ 6,40 	1,00	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	12
7	Café Torrado e Moído 500g		Café forte e aromático	1	 R$ 14,90 	0,50	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	23
8	Biscoito Cream Cracker 400g		Crocante e leve	1	 R$ 7,20 	0,40	Peso	EXATO	11	Felix Carlos Ferreira	Médio	11
9	Batata 2kg		Hortaliça versátil para diversas receitas	1	 R$ 9,90 	2,00	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	32
10	Tomate 1kg		Fresco, ideal para saladas e molhos	1	 R$ 7,80 	1,00	Peso	EXATO	11	Felix Carlos Ferreira	Alto	56
11	Leite Integral 1L		Fonte de cálcio e proteínas	1	 R$ 5,20 	1,03	Liquido	APROXIMADO	11	Felix Carlos Ferreira	Baixo 	73
12	Óleo de Soja 900ml		Óleo vegetal versátil	1	 R$ 6,40 	0,83	Liquido	APROXIMADO	11	Felix Carlos Ferreira	Baixo 	34
13	Suco de Laranja 1L		100% natural, sem conservantes	1	 R$ 6,90 	1,05	Liquido	APROXIMADO	11	Felix Carlos Ferreira	Baixo 	12
14	Refrigerante Cola 2L		Bebida gaseificada sabor cola	1	 R$ 8,50 	2,00	Liquido	APROXIMADO	11	Felix Carlos Ferreira	Baixo 	54
15	Água Mineral 1,5L		Natural e refrescante	1	 R$ 3,00 	1,50	Liquido	APROXIMADO	11	Felix Carlos Ferreira	Baixo 	12
16	Iogurte Natural 170g		Cremoso, fonte de probióticos	1	 R$ 2,80 	0,17	Peso	EXATO	11	Felix Carlos Ferreira	Baixo 	23
17	Queijo Mussarela 500g		Fatiado, sabor suave	1	 R$ 18,90 	0,50	Peso	EXATO	12	Jessica Souza Lima	Alto	
18	Carne Bovina (Patinho) 1kg		Corte magro, ideal para bifes	1	 R$ 39,90 	1,00	Peso	EXATO	12	Jessica Souza Lima	Alto	
19	Frango Inteiro 1,2kg		Carne branca, versátil	1	 R$ 24,90 	1,20	Peso	EXATO	12	Jessica Souza Lima	Alto	
20	Ovos Brancos 12 unidades		Fonte de proteína, embalagem com 12 unidades	1	 R$ 12,50 	0,72	Peso	EXATO	12	Jessica Souza Lima	Alto	
21	Arroz Integral 1kg		Grão longo, rico em fibras	1	 R$ 8,90 	1,00	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
22	Feijão Carioca 1kg		Tradicional, sabor marcante	1	 R$ 7,50 	1,00	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
23	Açúcar Refinado 1kg		Açúcar branco cristalizado	1	 R$ 5,10 	1,00	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
24	Sal Refinado 1kg		Sal de cozinha refinado	1	 R$ 3,20 	1,00	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
25	Macarrão Espaguete 500g		Massa tradicional para molhos	1	 R$ 4,70 	0,50	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
26	Farinha de Trigo 1kg		Base para pães, bolos e massas	1	 R$ 6,40 	1,00	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
27	Café Torrado e Moído 500g		Café forte e aromático	1	 R$ 14,90 	0,50	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
28	Biscoito Cream Cracker 400g		Crocante e leve	1	 R$ 7,20 	0,40	Peso	EXATO	12	Jessica Souza Lima	Baixo 	
29	Batata 2kg		Hortaliça versátil para diversas receitas	1	 R$ 9,90 	2,00	Peso	EXATO	13	Ruan Henrique Almeida	Baixo 	
30	Tomate 1kg		Fresco, ideal para saladas e molhos	1	 R$ 7,80 	1,00	Peso	EXATO	13	Ruan Henrique Almeida	Alto	
31	Leite Integral 1L		Fonte de cálcio e proteínas	1	 R$ 5,20 	1,03	Líquido	APROXIMADO	13	Ruan Henrique Almeida	Alto	
32	Óleo de Soja 900ml		Óleo vegetal versátil	1	 R$ 6,40 	0,83	Líquido	APROXIMADO	13	Ruan Henrique Almeida	Baixo 	
33	Suco de Laranja 1L		100% natural, sem conservantes	1	 R$ 6,90 	1,05	Líquido	APROXIMADO	13	Ruan Henrique Almeida	Alto	
34	Refrigerante Cola 2L		Bebida gaseificada sabor cola	1	 R$ 8,50 	2,00	Líquido	APROXIMADO	13	Ruan Henrique Almeida	Baixo 	
35	Água Mineral 1,5L		Natural e refrescante	1	 R$ 3,00 	1,50	Líquido	APROXIMADO	13	Ruan Henrique Almeida	Baixo 	
36	Iogurte Natural 170g		Cremoso, fonte de probióticos	1	 R$ 2,80 	0,17	Peso	EXATO	13	Ruan Henrique Almeida	Alto	
37	Queijo Mussarela 500g		Fatiado, sabor suave	1	 R$ 18,90 	0,50	Peso	EXATO	13	Ruan Henrique Almeida	Alto	
38	Carne Bovina (Patinho) 1kg		Corte magro, ideal para bifes	1	 R$ 39,90 	1,00	Peso	EXATO	13	Ruan Henrique Almeida	Alto	
39	Frango Inteiro 1,2kg		Carne branca, versátil	1	 R$ 24,90 	1,20	Peso	EXATO	13	Ruan Henrique Almeida	Alto	
40	Ovos Brancos 12 unidades		Fonte de proteína, embalagem com 12	1	 R$ 12,50 	0,72	Peso	APROXIMADO	13	Ruan Henrique Almeida	Alto	


