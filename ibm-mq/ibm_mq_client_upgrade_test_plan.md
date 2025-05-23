
# IBM MQ Client Upgrade Test Plan

## Objective
Ensure upgraded IBM MQ client works correctly on RHEL with existing MQ servers and integrations.

## Scope
- **In**: MQ client upgrade on RHEL, connectivity, messaging, SSL, integration checks
- **Out**: Non-RHEL systems, MQ server upgrades, app code changes

## Environment
- OS: RHEL 8
- MQ Client: v9.3 → v9.4
- MQ Server: MQ v9.2 or v9.3
- Tools: systemd services, CLI tools, logs

## Test Areas

1. **Installation**
   - Install and upgrade using RPM/yum
   - Validate rollback

2. **Connectivity**
   - Connect to remote MQ servers
   - Verify port and channel configs

3. **Messaging**
   - Produce/consume test messages
   - Verify persistence and queue depth

4. **Security**
   - SSL/TLS tests
   - Certificate and auth validation

5. **System Integration**
   - Test systemd services
   - Validate app integration and error logs

6. **Monitoring**
   - Ensure logs are collected
   - Validate resource usage with `top`, `ps`

7. **Performance**
   - Compare pre/post-upgrade throughput

## Data
- Types: XML, JSON, plain text
- Sizes: 1KB to 10MB
- Load: ~10,000 messages

## Pass Criteria
- No install/upgrade errors
- Stable connectivity and messaging
- Functional integration
- No major performance regressions

## Risks
- Config issues → Pre-validation
- Downtime → Prepare rollback script

## Rollback
1. Stop MQ-related services
2. Remove v9.4 RPMs
3. Reinstall v9.3
4. Restore config files