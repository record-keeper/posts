# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-03T08:00:01.995186+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×41 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×41 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×14 (24h)
- 🟡 FINAL_MISSING×12 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-03T07:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1807 actual=0.1818 gap=-0.0012`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S00: n=185 hit%=26.5% hit_CI[Bonf]=[18.3,36.7]% ROI=0.87 ROI_boot95=[0.63,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S01_NAKAANA1: n=191 hit%=24.1% hit_CI[Bonf]=[16.4,34.0]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=191<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=40.0% hit_CI[Bonf]=[25.9,56.0]% ROI=0.68 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-03T06:00:42]
- key: `ORPHAN_SCAN|191 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=15.8% ROI=0.48 (コスト 11,000/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.90 (コスト 10,100/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=97 hit%=26.8% ROI=0.89 (コスト 22,200/回収 19,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=51 hit%=23.5% ROI=0.46 (コスト 11,500/回収 5,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift ≥+30%: n=41 hit%=19.5% ROI=0.87 (コスト 11,200/回収 9,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|bt=win: n=456 pred=0.4723 actual=0.2785 error=+0.1938 (+41%) brier=0.2405 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|S00(win): n=185 pred=0.4216 hit=0.2649 cal_err=+0.1567 brier=0.2201 BSS=-0.13 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=191 pred=0.4887 hit=0.2408 cal_err=+0.2478 brier=0.2500 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=80 pred=0.5506 hit=0.4000 cal_err=+0.1506 brier=0.2646 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=7 pred=0.1233 actual=0.0000 gap=+0.1233`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.17MB / last modified 2026-09-03T08:00:04.925050+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
[INFO] run_cycle: === run_cycle 23:56:03 ===
2026-09-02 23:56:03,726 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 23:56:03,726 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 23:56:03,773 [INFO] predictor: Models loaded OK
2026-09-02 23:56:03,777 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 23:57:03,810 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-09-02 23:57:03,810 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 23:57:03,810 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 23:57:03,855 [INFO] predictor: Models loaded OK
2026-09-02 23:57:03,859 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 23:58:03,833 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-09-02 23:58:03,833 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 23:58:03,833 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 23:58:03,862 [INFO] predictor: Models loaded OK
2026-09-02 23:58:03,864 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 23:59:03,661 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-09-02 23:59:03,661 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 23:59:03,661 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 23:59:03,695 [INFO] predictor: Models loaded OK
2026-09-02 23:59:03,697 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-03 08:00:06,996 [INFO] run_cycle: === run_cycle 08:00:06 ===
2026-09-03 08:00:06,998 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-03 08:00:06,998 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-03 08:00:06,999 [INFO] run_cycle: Morning schedule load...

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 69
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 69
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 18, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 82
  PSI_DRIFT_DETECTED: 41
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 14
  FINAL_MISSING: 12
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 14 | 15,600 | 12,660 | -2,940 | 0.812 |
| S01_NAKAANA1 | 38 | 6 | 7,600 | 2,820 | -4,780 | 0.371 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 2,660 | -740 | 0.782 |

## 直近アラート (24h・新しい順)
```
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 7600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 2820, "roi_7d": 0.371, "sid": "S01_NAKAANA1"}
[06:00:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 349, "n_recent": 107, "psi": 0.349}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:38:04] FINAL_MISSING: {"deadline": "2026-09-02T16:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090217111605", "sid": "S00"}
[23:37:03] CIRCUIT_BREAKER_TRIP: {"cost": 7600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 2820, "roi_7d": 0.371, "sid": "S01_NAKAANA1"}
[23:27:04] FINAL_MISSING: {"deadline": "2026-09-02T19:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090224061956", "sid": "S00"}
[23:10:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:10:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:08:03] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 349, "n_recent": 107, "psi": 0.349}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 129R | win | 1 | 0.4111 | 6.0 | 2.47 | 300 | scan=- drift=- | 18:52:18 |
| S00 | 206R | win | 1 | 0.4111 | 7.8 | 3.21 | 300 | scan=12.7 drift=-38.6% | 17:31:18 |
| S00 | 126R | win | 1 | 0.3177 | 7.4 | 2.35 | 300 | scan=4.1 drift=+80.5% | 17:26:18 |
| S00 | 204R | win | 1 | 0.3177 | 4.1 | 1.30 | 300 | scan=- drift=- | 16:34:29 |
| S00 | 123R | win | 1 | 0.3177 | 14.3 | 4.54 | 300 | scan=- drift=- | 16:03:25 |
| S00 | 179R | win | 1 | 0.0448 | 4.2 | 0.19 | 300 | scan=- drift=- | 15:01:19 |
| S02_TETSUBAN | 168R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 14:53:19 |
| S00 | 227R | win | 1 | 0.5735 | 4.9 | 2.81 | 300 | scan=4.8 drift=+2.1% | 14:40:43 |
| S01_NAKAANA1 | 057R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=3.0 drift=+23.3% | 14:29:19 |
| S00 | 066R | win | 1 | 0.5174 | 9.5 | 4.92 | 300 | scan=13.0 drift=-26.9% | 13:42:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +9.4% | -73.7% | +158.3% | 16 | 10 | 42 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 462.2s |
| **Latency** (scan→final max) | 593.9s |
| **Traffic** (notifications 24h) | 69 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 456 | 0.4723 | 0.2785 | +0.1938 | 🟡+41% | 0.2405 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 185 | 0.4216 | 0.2649 | 0.2201 | 🔴-0.13 | 0.866 |
| S01_NAKAANA1 | win | 191 | 0.4887 | 0.2408 | 0.2500 | 🔴-0.37 | 0.734 |
| S02_TETSUBAN | win | 80 | 0.5506 | 0.4000 | 0.2646 | 🔴-0.10 | 0.682 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1233 | 0.0000 | 🔴+0.1233 |
| 0.15-0.20 | 11 | 0.1807 | 0.1818 | ✅-0.0012 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 159 | 0.4053 | 0.2453 | 🔴+0.1600 |
| 0.50+ | 267 | 0.5462 | 0.3109 | 🔴+0.2354 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 127 | 0.776 |
| win | <5.0 | ✅learned | 232 | 0.741 |
| win | <10.0 | ✅learned | 112 | 0.457 |
| win | <20.0 | ✅learned | 31 | 0.231 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-09-03T08:00:01.995186+09:00_