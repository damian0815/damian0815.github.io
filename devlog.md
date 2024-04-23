# Devlog

## 23 April 2024

### Making audiocraft magnet work on MPS

* identified that the token outputs on MPS and CPU differ
* rechecked differing with fixed seed
* identified that the token outputs differ after "1" step (actually: 4 steps, but i don't understand the steps yet)
* identified that the conditioning inputs are the same, so the problem is after conditioning
* **first appearance of difference** is at sampling, in `lm_magnet.py`, `_generate_stage`. mps results in different values
  -> no it's not, there's just an unhandled RNG.
  -> add torch.generator arg to `utils.sample_top_p`
  -> no, don't do that, because torch.generator needs to be on same device as tensors and MPS rng will be different to CPU RNG.
  -> ok, instead just disable sampling
* **good news**: issue is in converting samples to wav, not in sampling. how do I know? ran 2x tests with same seed - output tokens are identical but output audio on MPS is scrambled.
  

