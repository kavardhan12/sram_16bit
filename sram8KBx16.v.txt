module sram8KBx16 #(
  parameter  AW       = 13 // Address width MAX Implementable upto 1KB and MAX Synthesizable upto 8KB
  //parameter  filename = "data.hex"
  )
 (
  input  wire               clk,
  input  wire               rst,
  input  wire  [AW-1:0]     Address,
  //inout  wire  [15:0]       DataIO,
  input  wire  [15:0]       DataIO,
  input  wire               WEn,
  input  wire               OEn,
  input  wire               CEn,
  input  wire               LBn,
  input  wire               UBn,
  output wire   [15:0]      data      
  );

reg    [7:0]         ram_data[0:((1<<AW)-1)]; // 256k byte of RAM data MAX at simulation level
integer              i;                 // Loop counter
wire                 out_enable_lb;       // Lower byte output enable
wire                 out_enable_ub;       // Upper byte output enable
wire   [AW-1:0]      array_addr;
reg    [15:0]        read_data;


// Start of main code
// Initialize RAM
initial
  begin
  for (i=0;i<(1<<AW);i=i+1) 
    begin
    ram_data[i] = 8'h00; //Initialize all data to 0
    end
  /*if (filename != "")
    begin
    $readmemh(filename, ram_data); // Then read in program code
    end*/
  end

// Read control
assign array_addr   = {Address[AW-1:1], 1'b0};

// Read from array
always @ (posedge clk)
begin
if(rst)
begin
    read_data[7:0] = 8'h00;
    read_data[15:8] = 8'h00;
end
else
begin
  if ((WEn) & (~OEn) & (~CEn))
    begin
    read_data[7:0] = ram_data[array_addr];
    read_data[15:8] = ram_data[array_addr+1];
    end
  else
    begin
    read_data[7:0] = 8'hxx;
    read_data[15:8] = 8'hxx;
    end
    
end
end
    assign data[15:0] = {read_data[15:8],read_data[7:0]};


// Write
always @(posedge clk)
begin
if(rst)
begin
 ram_data[array_addr] =8'h00;
end
else
begin
  if ((~WEn) & (~CEn) & (DataIO))
    begin
    if (~LBn)
      begin
      ram_data[array_addr] = DataIO[7:0];
      end
    if (~UBn)
      begin
      ram_data[array_addr+1] = DataIO[15:8];
      end
    end
end
end



endmodule
