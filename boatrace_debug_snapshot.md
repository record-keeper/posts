# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-24T04:10:01.928891+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×51  [2026-05-23T23:09:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×51  [2026-05-23T23:09:06]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×30  [2026-05-23T18:21:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-05-23T11:10:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×43  [2026-05-23T10:00:10]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-05-23T06:00:10]
- key: `ORPHAN_SCAN|240 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1288 actual=0.2000 gap=-0.0712`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S00: n=196 hit%=28.6% hit_CI[Bonf]=[20.3,38.6]% ROI=0.96 ROI_boot95=[0.71,1.24]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=196<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=65 hit%=32.3% hit_CI[Bonf]=[18.4,50.2]% ROI=0.85 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=65<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=45.0% hit_CI[Bonf]=[25.2,66.5]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=50 hit%=32.0% ROI=0.86 (コスト 14,800/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=30.8% ROI=1.28 (コスト 9,300/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=59 hit%=27.1% ROI=0.92 (コスト 14,400/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=23 hit%=34.8% ROI=1.31 (コスト 5,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=18.4% ROI=0.51 (コスト 10,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|bt=win: n=301 pred=0.4570 actual=0.3156 error=+0.1414 (+31%) brier=0.2332 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.25MB / last modified 2026-05-24T04:00:04.885803+09:00

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
61 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 23:55:06,461 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 23:55:06,508 [INFO] predictor: Models loaded OK
2026-05-23 23:55:06,511 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-23 23:56:05,768 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-05-23 23:56:05,768 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 23:56:05,768 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 23:56:05,812 [INFO] predictor: Models loaded OK
2026-05-23 23:56:05,818 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-23 23:57:06,381 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-05-23 23:57:06,381 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 23:57:06,381 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 23:57:06,448 [INFO] predictor: Models loaded OK
2026-05-23 23:57:06,452 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-23 23:58:05,572 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-05-23 23:58:05,573 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 23:58:05,573 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 23:58:05,638 [INFO] predictor: Models loaded OK
2026-05-23 23:58:05,644 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-23 23:59:05,529 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-05-23 23:59:05,530 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 23:59:05,530 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 23:59:05,591 [INFO] predictor: Models loaded OK
2026-05-23 23:59:05,595 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 29, 'result': 11, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 121
  FINAL_MISSING: 32
  KS_ODDS_DRIFT: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 12 | 9,000 | 14,250 | +5,250 | 1.583 |
| S01_NAKAANA1 | 30 | 8 | 6,000 | 5,880 | -120 | 0.98 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 2,280 | -1,120 | 0.671 |

## 直近アラート (24h・新しい順)
```
[23:54:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 5.4e-05, "ks_stat": 0.296}
[23:54:06] FINAL_MISSING: {"deadline": "2026-05-23T19:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052315091923", "sid": "S00"}
[23:12:06] FINAL_MISSING: {"deadline": "2026-05-23T15:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052316101537", "sid": "S02_TETSUBAN"}
[23:09:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:07:06] FINAL_MISSING: {"deadline": "2026-05-23T11:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052309031129", "sid": "S00"}
[23:02:05] FINAL_MISSING: {"deadline": "2026-05-23T16:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052301031627", "sid": "S00"}
[22:54:05] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 5.4e-05, "ks_stat": 0.296}
[22:54:05] FINAL_MISSING: {"deadline": "2026-05-23T19:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052315091923", "sid": "S00"}
[22:11:06] FINAL_MISSING: {"deadline": "2026-05-23T15:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052316101537", "sid": "S02_TETSUBAN"}
[22:09:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
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
| S01_NAKAANA1 | 198R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.7 drift=-8.1% | 20:53:21 |
| S01_NAKAANA1 | 126R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=3.7 drift=-5.4% | 17:54:21 |
| S01_NAKAANA1 | 155R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=- drift=- | 17:34:32 |
| S02_TETSUBAN | 1111R | win | 1 | 0.4111 | 2.2 | 0.90 | 200 | scan=2.2 drift=+0.0% | 15:57:21 |
| S02_TETSUBAN | 057R | win | 1 | 0.5334 | 2.6 | 1.39 | 200 | scan=- drift=- | 14:39:21 |
| S01_NAKAANA1 | 096R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=- drift=- | 12:59:21 |
| S02_TETSUBAN | 053R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 12:41:46 |
| S02_TETSUBAN | 114R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=2.1 drift=+28.6% | 11:54:32 |
| S01_NAKAANA1 | 108R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=4.9 drift=-28.6% | 11:50:35 |
| S00 | 237R | win | 1 | 0.4989 | 4.5 | 2.25 | 300 | scan=6.0 drift=-25.0% | 11:12:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | +2.6% | -74.9% | +148.9% | 15 | 7 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 435.4s |
| **Latency** (scan→final max) | 638.4s |
| **Traffic** (notifications 24h) | 69 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 309 | 0.4573 | 0.3204 | +0.1369 | 🟡+30% | 0.2352 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 195 | 0.4357 | 0.2923 | 0.2277 | 🔴-0.10 | 0.983 |
| S01_NAKAANA1 | win | 70 | 0.4845 | 0.3143 | 0.2442 | 🔴-0.13 | 0.821 |
| S02_TETSUBAN | win | 44 | 0.5098 | 0.4545 | 0.2540 | 🔴-0.02 | 0.827 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0041 | 0.0769 | 🔴-0.0729 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 138 | 0.4189 | 0.2609 | 🔴+0.1580 |
| 0.50+ | 146 | 0.5402 | 0.3904 | 🔴+0.1498 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 20 | 0.744 |
| win | <5.0 | ✅learned | 38 | 0.802 |
| win | <10.0 | ✅learned | 34 | 0.547 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-24T04:10:01.928891+09:00_