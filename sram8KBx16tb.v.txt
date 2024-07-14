module sram8KBx16tb();
parameter  AW       = 13;
  reg clk;
  reg rst;
  reg [AW-1:0]Address;
  reg [15:0] DataIO;
  reg WEn;
  reg OEn;
  reg CEn;
  reg LBn;
  reg UBn;
  wire [15:0] data; 
  integer i;
  integer k;
initial 
begin
clk=0;
forever #5 clk = ~clk;
end
initial 
begin
rst=1;
#10 rst=0;
end

initial begin
Address=12'b000000000000;
DataIO=16'h0000;
end


//port map
sram8KBx16  #(
.AW(13)
)
sram8KBx16 (
.clk(clk),
.rst(rst),
.Address(Address),
.DataIO(DataIO),
.WEn(WEn),
.OEn(OEn),
.CEn(CEn),
.LBn(LBn),
.UBn(UBn),
.data(data)
);


initial
begin

//write
/*for(i=0;i<=6144;i=i+1)
begin
#10
WEn=1'b0;
CEn=1'b0;
LBn=1'b0;
OEn=1'b1;
UBn=1'b0;
DataIO=DataIO+16'h0001;
Address=Address+12'h002;
end*/
//read 12'b000000000000 address



WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000000;
//read rest addresses
for(k=0;k<=4100;k=k+1)
begin
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=Address+12'h002;
end

//iterative test cases
/*#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000001;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000010;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000101;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000100;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000101;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000110;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000111;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000001000;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000001001;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000001010;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000001011;
#20
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000001100;*/
//end
end


//iterative test cases
//end
/*initial
begin
WEn=1'b0;
CEn=1'b0;
LBn=1'b0;
OEn=1'b1;
UBn=1'b0;
DataIO=16'h1234;
Address=12'b000000000011;
#30
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000000011;
#30
WEn=1'b0;
CEn=1'b0;
LBn=1'b0;
OEn=1'b1;
UBn=1'b0;
DataIO=16'h1010;
Address=12'b000000001111;
#30
WEn=1'b1;
OEn=1'b0;
CEn=1'b0;
LBn=1'b1;
UBn=1'b1;
Address=12'b000000001111;*/
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000000000001;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000000000011;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000000000111;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000000000001;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000000001111;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000000000001;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000000111111;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000001111111;
//#2
//WEn=1'b1;
//OEn=1'b0;
//CEn=1'b0;
//Address=12'b000011111111;



//end



endmodule