# fedora-coreos-streams

Official stream metadata for Fedora CoreOS created by the
[generator](https://github.com/coreos/fedora-coreos-stream-generator/).

## Stream metadata

Latest FCOS stream metadata for different streams are available under the
`streams/` directory. To generate the latest stream metadata for the `testing`
stream, run:

```
fedora-coreos-stream-generator -releases=https://builds.coreos.fedoraproject.org/prod/streams/testing/releases.json -output-file=streams/testing.json -pretty-print
```

## How to do a Fedora CoreOS release

### Prerequisites for performing a release

- Access to the official [CentOS CI fedora-coreos namespace](https://jenkins-fedora-coreos.apps.ocp.ci.centos.org/)

### Release checklist

The steps for doing a release are in the tickets created in the
[coreos/fedora-coreos-streams](https://github.com/coreos/fedora-coreos-streams/)
repository. An overview of the process can be seen in
[this video](https://dustymabe.fedorapeople.org/videos/2021-10-04_FCOS-Release-Process.mp4).

Those issues are generally created at the end of the previous release but if
you need to manually create one, you can use the following links:
- [stable](https://github.com/coreos/fedora-coreos-streams/issues/new?labels=kind/release,jira&template=stable.md)
- [testing](https://github.com/coreos/fedora-coreos-streams/issues/new?labels=kind/release,jira&template=testing.md)
- [next](https://github.com/coreos/fedora-coreos-streams/issues/new?labels=kind/release,jira&template=next.md)

### Pipeline failures & recovery

If a part of a pipeline run fails there may be options available that don't
require you to start from the very beginning.

- fedora-coreos-pipeline
    - if the top level pipeline fails you'll need to restart it likely
      with FORCE checked in the build parameters.
- multi-arch-pipeline
    - Assuming the top level pipeline passed you can start another multi-arch
      pipeline run with the exact same parameters as the original multi-arch
      pipeline run that was automatically kicked off by top level pipeline.
        - Open the failed job and look at the build parameters that were used.
        - Start a new job copy and pasting the exact build parameters.
- kola-{aws,gcp,openstack}
    - These jobs are just tests, that don't produce any artifacts.
    - If one of these jobs fail you can start a new job, but make
      sure to use the exact same build parameters as the original failed job.

### Release managers

FCOS release managers are not part of the normal release rotation but pay
attention to most releases and make sure they are progressing (PR reviews,
debugging issues). They also volunteer (or find a volunteer) to execute ad-hoc
releases that are outside of the normal schedule. The current release managers
are:

- Dusty Mabe
- Jonathan Lebon

### Release executors

The current set of release executors are (in alphabetical order, see below for
the rotation):

- Benjamin Gilbert
- Clement Verna
- Luca Bruno
- Renata Ravanelli
- Saqib Ali
- Sinny Kumari
- Sohan Kunkerkar
- Timothée Ravier

The build pipeline for releases will typically get started on Monday. Assuming
things go smoothly rollouts will start on Tuesday. If there are any conflicts
in the schedule we can easily swap a rotation with someone else.

### Current release schedule

See the schedule in <https://hackmd.io/WCA8XqAoRvafnja01JG_YA>
