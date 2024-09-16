
``` mermaid
stateDiagram-v2
    state monitor {
        [*] --> monitor_init
        monitor_init --> monitor_sshLog : monitor_done
        monitor_sshLog --> monitor_packet : monitor_done
        monitor_packet --> monitor : monitor_done
    }
    state detect {
        [*] --> detect_init
        detect_init --> detect_sshLog : detect_done
        detect_sshLog --> detect_packet : detect_done
    }
    state defend {
        [*] --> defend_init
        defend_init --> defend_sshLog : defend_done
        defend_sshLog --> defend_packet : defend_done
    }
    monitor --> detect : monitor_done [is_sshLogChanged]
    monitor --> detect : monitor_done [is_packet]
    detect --> defend : detect_done [is_sshLogChanged]
    detect --> defend : detect_done [is_packet]
    defend --> monitor : defend_done [is_sshLogChanged]
    defend --> monitor : defend_done [is_packet]
    detect_packet --> defend : detect_done
    detect_packet --> monitor : detect_done
    defend_packet --> monitor : defend_done

```
