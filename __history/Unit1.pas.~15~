unit Unit1;

interface

uses
  Winapi.Windows, Winapi.Messages, System.SysUtils, System.Variants, System.Classes, Vcl.Graphics,
  Vcl.Controls, Vcl.Forms, Vcl.Dialogs, Vcl.StdCtrls, System.Threading;

type
  TForm1 = class(TForm)
    Label1: TLabel;
    Button1: TButton;
    Button2: TButton;
    Button3: TButton;
    Label2: TLabel;
    Label3: TLabel;
    Label4: TLabel;
    Button4: TButton;
    Button5: TButton;
    Button6: TButton;
    procedure Button1Click(Sender: TObject);
    procedure Button2Click(Sender: TObject);
    procedure Button3Click(Sender: TObject);
    procedure Button4Click(Sender: TObject);
    procedure Button5Click(Sender: TObject);
  private
    { Private declarations }
    procedure Teste;
  public
    { Public declarations }
  end;

var
  Form1: TForm1;
  a : IFuture<String>;
  b : IFuture<String>;
  c : IFuture<String>;

implementation

{$R *.dfm}

{ TForm1 }

procedure TForm1.Button1Click(Sender: TObject);
begin
  Sleep(10000);
  Label1.Caption := DateTimeToStr(Now);
end;

procedure TForm1.Button2Click(Sender: TObject);
begin
  TTask.Run(procedure
  begin
    Sleep(10000);
    TThread.Synchronize(TThread.CurrentThread,
    procedure
    begin
      Label1.Caption := DateTimeToStr(Now);
    end);
  end);
end;

procedure TForm1.Button3Click(Sender: TObject);
var
  t2 : ITask;
begin
  t2 := TTask.Create(procedure
  begin
    Sleep(10000);
    TThread.Synchronize(TThread.CurrentThread,
    procedure
    begin
      Label1.Caption := DateTimeToStr(Now);
    end);
  end);

  t2.Start;

end;

procedure TForm1.Button4Click(Sender: TObject);
var
  a, b, c : String;
  tempo : Cardinal;
begin

  tempo := GetTickCount;

  Sleep(5000);
  a := Random(100).ToString;

  Sleep(3000);
  b := Random(100).ToString;

  Sleep(2000);
  c := Random(100).ToString;

  tempo := GetTickCount - tempo;

  label2.Caption := 'Tepo gasto: ' + IntToStr(tempo) + 'ms Valor: ' + a + ' ' + b + ' ' + c;

end;

procedure TForm1.Button5Click(Sender: TObject);
begin
  TTask.Run(
  procedure
  var
    tempo : Cardinal;
  begin
    tempo := GetTickCount;

    a := TTask.Future<String>(
      function : String
      begin
        Sleep(5000);
        Result := Random(100).ToString;
      end);

    b := TTask.Future<String>(
      function : String
      begin
        Sleep(3000);
        Result := Random(100).ToString;
      end);

    c := TTask.Future<String>(
      function : String
      begin
        Sleep(2000);
        Result := Random(100).ToString;
      end);

    TThread.Synchronize(TThread.CurrentThread,
    procedure
    begin
      tempo := GetTickCount - tempo;

      label3.Caption := 'Tepo gasto: ' + IntToStr(tempo) + 'ms Valor: ' + a.Value + ' ' + b.Value + ' ' + c.Value;
    end);

  end);
end;

procedure TForm1.Teste;
begin
  Label1.Caption := 'Teste';
end;

end.
