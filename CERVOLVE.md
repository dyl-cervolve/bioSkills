# Cervolve / Jetty lipidomics profile

This fork preserves GPTomics/bioSkills and its MIT license. The upstream is
archived; this fork is a maintained snapshot for Cervolve use, with no assumption
of upstream support. `dyl-cervolve/brain-omics-ingestion` pins the reviewed commit.

Jetty discovers only the `metabolomics` subtree through the consumer's explicit
allowlist. Start with `metabolomics/lipidomics/SKILL.md`; assess metabolite
annotation, normalization/QC and statistical-analysis skills as applicable.
Retain their relative references and examples. R/lipidr examples are optional
analysis guidance: the Python retrieval environment does not install R,
Bioconductor, MS-DIAL or commercial LipidSearch.

The ingestion contract takes precedence over analysis defaults:

* Retrieve actual lipid-feature abundance tables and sample/assay metadata.
  Preserve deposited values, zeros, missingness and original feature names.
* Parse names with pygoslin, retaining the source name and parse status. A
  successful parse does not prove sn-position, double-bond location or isomer
  identity. Never add structural resolution unsupported by source evidence.
* Keep ambiguous names and unknown features; record mapping limitations rather
  than silently discarding or collapsing them. Keep assay mode, units and
  measurement availability explicit when combining positive/negative runs.
* Record internal-standard and normalization provenance. Do not turn relative
  intensities into absolute concentrations without source calibration.
* Keep donor-linked observations in one ML partition; fit preprocessing on the
  training partition. Preserve original measurements in the canonical matrix.
* Follow Jetty's 8 GB, 4 GB source-set and 60-minute limits. Processed-table
  retrieval is the default; raw-spectrum processing requires a separate setup.
* Write evidence-backed skill decisions and typed `checks[]` validation entries.

Use `https://github.com/dyl-cervolve/brain-omics-ingestion` for the locked Python
dependencies and Jetty bootstrap. Skills are Markdown guidance, not pip packages.
Inspect helper code before execution. New tools, including LipidLibrarian,
LipidLynxX and LipidFinder, need separate dependency and license review before
they are added to the locked environment.
