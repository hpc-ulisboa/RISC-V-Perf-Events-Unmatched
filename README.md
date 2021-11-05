# RISC-V-Perf-Events-Unmatched

The series of patches available in this respository add raw event matching between perf and any risc-v cpu.
This work introduces support for the events of the HiFive Unmatched board.

## Please cite

A prior version of this work is documented in https://carrv.github.io/2021/papers/CARRV2021_paper_29_Domingos.pdf.
If you use this series of patches for your work, please cite it

## License

This work is licensed under GNU GPL 2.0.

## Prints

### Perf list output (cropped to pmu), for the HiFive Unmatched board:
>       instructions:
>        atomic_memory_retired
>             [Atomic memory operation retired]
>        conditional_branch_retired
>             [Conditional branch retired]
>        exception_taken
>             [Exception taken]
>        fp_addition_retired
>             [Floating-point addition retired]
>        fp_div_sqrt_retired
>             [Floating-point division or square-root retired]
>        fp_fusedmadd_retired
>             [Floating-point fused multiply-add retired]
>        fp_load_retired
>             [Floating-point load instruction retired]
>        fp_multiplication_retired
>             [Floating-point multiplication retired]
>        fp_store_retired
>             [Floating-point store instruction retired]
>        integer_arithmetic_retired
>             [Integer arithmetic instruction retired]
>        integer_division_retired
>             [Integer division instruction retired]
>        integer_load_retired
>             [Integer load instruction retired]
>        integer_multiplication_retired
>             [Integer multiplication instruction retired]
>        integer_store_retired
>             [Integer store instruction retired]
>        jal_instruction_retired
>             [JAL instruction retired]
>        jalr_instruction_retired
>             [JALR instruction retired]
>        other_fp_retired
>             [Other floating-point instruction retired]
>        system_instruction_retired
>             [System instruction retired]
>      
>      memory:
>        data_tlb_miss
>             [Data TLB miss]
>        dcache_miss_mmio_accesses
>             [Data cache miss or memory-mapped I/O access]
>        dcache_writeback
>             [Data cache write-back]
>        icache_retired
>             [Instruction cache miss]
>        inst_tlb_miss
>             [Instruction TLB miss]
>        utlb_miss
>             [UTLB miss]
>      
>      microarch:
>        addressgen_interlock
>             [Address-generation interlock]
>        branch_direction_misprediction
>             [Branch direction misprediction]
>        branch_target_misprediction
>             [Branch/jump target misprediction]
>        csr_read_interlock
>             [CSR read interlock]
>        dcache_dtim_busy
>             [Data cache/DTIM busy]
>        fp_interlock
>             [Floating-point interlock]
>        icache_itim_busy
>             [Instruction cache/ITIM busy]
>        integer_multiplication_interlock
>             [Integer multiplication interlock]
>        longlat_interlock
>             [Long-latency interlock]
>        pipe_flush_csr_write
>             [Pipeline flush from CSR write]
>        pipe_flush_other_event
>             [Pipeline flush from other event]


### Perf stat output:

>     perf stat -eexception_taken,integer_load_retired,integer_store_retired,atomic_memory_retired,system_instruction_retired,integer_arithmetic_retired,conditional_branch_retired,jal_instruction_retired,jalr_instruction_retired,integer_multiplication_retired,integer_division_retired,fp_load_retired,fp_store_retired,fp_addition_retired,fp_multiplication_retired,fp_fusedmadd_retired,fp_div_sqrt_retired,other_fp_retired,data_tlb_miss,dcache_miss_mmio_accesses,dcache_writeback,icache_retired,inst_tlb_miss,utlb_miss,addressgen_interlock,longlat_interlock,csr_read_interlock,icache_itim_busy,dcache_dtim_busy,branch_direction_misprediction,branch_target_misprediction,pipe_flush_csr_write,pipe_flush_other_event,integer_multiplication_interlock,fp_interlock stress-ng --cpu 1 --cpu-method trig -t 60s
>     stress-ng: info:  [500] setting to a 60 second run per stressor
>     stress-ng: info:  [500] dispatching hogs: 1 cpu
>     stress-ng: info:  [500] successful run completed in 60.02s (1 min, 0.02 secs)
>    
>       Performance counter stats for 'stress-ng --cpu 1 --cpu-method trig -t 60s':
>
>            233185      exception_taken                                               (5.72%)
>        5010843878      integer_load_retired                                          (5.73%)
>        4437123760      integer_store_retired                                         (5.73%)
>            875636      atomic_memory_retired                                         (5.72%)
>         787401517      system_instruction_retired                                     (5.73%)
>       58176497169      integer_arithmetic_retired                                     (5.74%)
>        9689155944      conditional_branch_retired                                     (5.73%)
>        2141143732      jal_instruction_retired                                       (5.72%)
>         624939326      jalr_instruction_retired                                      (5.72%)
>        1900272300      integer_multiplication_retired                                     (5.72%)
>          29231344      integer_division_retired                                      (5.72%)
>        1672274835      fp_load_retired                                               (5.73%)
>         592215149      fp_store_retired                                              (5.73%)
>          13592616      fp_addition_retired                                           (5.73%)
>          13597374      fp_multiplication_retired                                     (5.72%)
>        1331957808      fp_fusedmadd_retired                                          (5.72%)
>         592410829      fp_div_sqrt_retired                                           (5.72%)
>         227334317      other_fp_retired                                              (5.72%)
>          95772283      data_tlb_miss                                                 (5.72%)
>           6291088      dcache_miss_mmio_accesses                                     (5.72%)
>             55591      dcache_writeback                                              (5.72%)
>          47394708      icache_retired                                                (5.72%)
>          62778259      inst_tlb_miss                                                 (5.72%)
>          10159938      utlb_miss                                                     (5.72%)
>         424446212      addressgen_interlock                                          (5.72%)
>         849061809      longlat_interlock                                             (5.72%)
>                 0      csr_read_interlock                                            (5.71%)
>       16924613138      icache_itim_busy                                              (5.71%)
>         204163844      dcache_dtim_busy                                              (5.70%)
>         175163620      branch_direction_misprediction                                     (5.72%)
>         202874026      branch_target_misprediction                                     (5.71%)
>         433228932      pipe_flush_csr_write                                          (5.71%)
>                 0      pipe_flush_other_event                                        (5.71%)
>         429384915      integer_multiplication_interlock                                     (5.71%)
>        8635530214      fp_interlock                                                  (5.71%)
>
>      60.044837787 seconds time elapsed
>
>      60.001431000 seconds user
>       0.033660000 seconds sys
