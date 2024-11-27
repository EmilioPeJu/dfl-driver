# DFL FPGA Loader

Small driver to program a 7-series xilinx FPGA by bitbanging the bitstream over
a serial-like interface.

Example device tree node:
```dts
    load_fpga: dfl {
        compatible = "dls,fpga_loader";
        dev_name = "load_fpga";
        pinctrl-names = "default";
        pinctrl-0 = <&pinctrl_dls_fpga>;
        init-gpios = <&gpio0 7 GPIO_ACTIVE_HIGH>;
        done-gpios = <&gpio3 30 GPIO_ACTIVE_HIGH>;
        prog-gpios = <&gpio3 31 GPIO_ACTIVE_HIGH>;
        d0-gpios = <&gpio3 22 GPIO_ACTIVE_HIGH>;
        clk-gpios = <&gpio3 23 GPIO_ACTIVE_HIGH>;
        status = "okay";
    };
```

In this example, the driver will create a device `/dev/load_fpga` which can
be used to load the bin bitstream, e.g. `cat bitstream.bin > /dev/load_fpga`
